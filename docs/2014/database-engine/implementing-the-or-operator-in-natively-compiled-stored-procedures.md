---
title: Implementar el operador OR en procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2528e74-2b1c-48cb-861b-c4e57b51ac35
author: stevestein
ms.author: sstein
ms.openlocfilehash: 52c3a38488117c55de497442dd138a55cc8b32e4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932856"
---
# <a name="implementing-the-or-operator-in-natively-compiled-stored-procedures"></a>Implementar el operador OR en procedimientos almacenados compilados de forma nativa
  No se admiten operadores OR en predicados de consulta en procedimientos almacenados compilados de forma nativa. Puesto que tampoco se admiten operadores NOT en los predicados de consulta en los procedimientos almacenados compilados de forma nativa, los efectos de los operadores OR no se pueden simular mediante el uso de operadores lógicos equivalentes solamente. Sin embargo, los efectos de un operador OR se pueden simular con variables de tabla optimizada para memoria.  
  
## <a name="or-operator-in-where-clause"></a>Operador OR en una cláusula WHERE  
 Si tiene un operador OR en una cláusula WHERE, puede usar el método siguiente para simular su comportamiento:  
  
1.  Cree una variable de tabla optimizada para memoria con el esquema correspondiente. Para ello se necesita un tipo de tabla optimizada para memoria predefinido.  
  
2.  Empezando por el operador OR de nivel superior, separe la cláusula WHERE en dos partes según los predicados combinados mediante el operador OR. Si tiene más de un operador OR en una cláusula WHERE, puede ser necesario hacerlo más de una vez. Repita este paso hasta que no queden operadores OR. Por ejemplo, si tiene el predicado siguiente:  
  
    ```  
    pred1 OR (pred2 AND (pred3 OR pred4)) OR (pred5 AND pred6)  
    ```  
  
     Después de este paso, debe tener los predicados siguientes:  
  
    ```  
    pred1  
    pred5 AND pred6  
    pred2 AND pred3  
    pred2 AND pred4  
    ```  
  
3.  Ejecute una consulta con cada una de las dos partes del paso 2 como predicado. Inserte el resultado de cada consulta en la variable de tabla optimizada para memoria creada en el paso 1.  
  
4.  Si es necesario, quite los duplicados de la variable de tabla optimizada para memoria.  
  
5.  Use el contenido de la variable de tabla optimizada para memoria como el resultado de la consulta.  
  
 En el ejemplo siguiente se usan tablas de la base de datos AdventureWorks2012 que se actualizaron para [!INCLUDE[hek_2](../includes/hek-2-md.md)]. Para descargar los archivos de este ejemplo, vaya a [bases de datos de AdventureWorks: 2012, 2008R2 y 2008](https://msftdbprodsamples.codeplex.com/releases/view/93587). Para aplicar el [!INCLUDE[hek_2](../includes/hek-2-md.md)] ejemplo de código a AdventureWorks2012, vaya a [SQL Server 2014 en el ejemplo de OLTP en memoria](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Agregue el procedimiento almacenado siguiente a la base de datos. Convertiremos este procedimiento almacenado para que use compilación nativa.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_ondisk  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
AS BEGIN  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  WHERE  s.SalesOrderId = @SalesOrderId  
      OR s.SalesOrderDetailId = @SalesOrderDetailId  
      OR s.CarrierTrackingNumber = @CarrierTrackingNumber  
      OR s.ProductID = @ProductId  
      OR (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
END  
GO  
```  
  
 Después de la conversión, el esquema de tabla y de procedimiento almacenado es el siguiente:  
  
```  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesOrderDetailType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailTempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  recordcount int not null  
  INDEX ix_fuzzySearchSalesOrderDetailTempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_inmem  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.fuzzySearchSalesOrderDetailType  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderId = @SalesOrderId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderDetailId = @SalesOrderDetailId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.CarrierTrackingNumber COLLATE Latin1_General_BIN2 = @CarrierTrackingNumber COLLATE Latin1_General_BIN2   
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.ProductID = @ProductId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
  
  -- After the above statements, there will be duplicates inside @retValue  
  -- Delete the duplicates from @retValue  
  DECLARE @duplicates Sales.fuzzySearchSalesOrderDetailTempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, recordcount)   
  SELECT SalesOrderId, SalesOrderDetailId, COUNT(*) AS recordCount  
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId  
  
  -- Now we have one row per pair  
  -- clear and rebuild the result set  
  DELETE FROM @retValue  
  
  INSERT INTO @retValue  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates d ON s.SalesOrderId = d.SalesOrderId AND s.SalesOrderDetailId = d.SalesOrderDetailId  
  
  -- After this every pair of (SalesOrderId, SalesOrderDetailId) in @retValue should be unique.  
  SELECT SalesorderId, SalesOrderDetailId, ModifiedDate FROM @retValue  
END  
GO  
```  
  
## <a name="or-operator-in-join-condition"></a>Operador OR en una condición JOIN  
 Si tiene un operador OR en una condición JOIN de una instrucción SELECT, puede usar el método siguiente para simular su comportamiento. Si tiene más de un operador OR en una condición JOIN o tiene varias condiciones JOIN con operadores OR, puede ser necesario hacerlo más de una vez.  
  
 Si tiene condiciones OUTER JOIN, puede combinar esta solución alternativa con la solución para las condiciones OUTER JOIN.  
  
1.  Cree una variable de tabla optimizada para memoria con el esquema correspondiente. Para ello se necesita un tipo de tabla optimizada para memoria predefinido.  
  
2.  Separe el predicado de la condición JOIN en dos partes según los predicados combinados mediante el operador OR. Si tiene varias condiciones JOIN, puede que necesite hacerlo para cada condición JOIN y crear después un conjunto de combinaciones de los fragmentos resultantes. Por ejemplo, si tiene tres condiciones JOIN con un operador OR en cada condición JOIN, puede tener 2x2x2=8 predicados.  
  
3.  Para cada predicado generado por el paso 2, cree una consulta que inserte su resultado en la variable de tabla optimizada para memoria creada en el paso 1.  
  
4.  Si es necesario, quite los duplicados de la variable de tabla optimizada para memoria.  
  
5.  Use el contenido de la variable de tabla optimizada para memoria como el resultado de la consulta.  
  
 En el ejemplo siguiente se usan tablas de la base de datos AdventureWorks2012 que se actualizaron para [!INCLUDE[hek_2](../includes/hek-2-md.md)]. Para descargar los archivos de este ejemplo, vaya a [bases de datos de AdventureWorks: 2012, 2008R2 y 2008](https://msftdbprodsamples.codeplex.com/releases/view/93587). Para aplicar el [!INCLUDE[hek_2](../includes/hek-2-md.md)] ejemplo de código a AdventureWorks2012, vaya a [SQL Server 2014 en el ejemplo de OLTP en memoria](https://msftdbprodsamples.codeplex.com/releases/view/114491).  
  
 Agregue el procedimiento almacenado siguiente a la base de datos. Convertiremos este procedimiento almacenado para que use compilación nativa. En este ejemplo se usan condiciones INNER JOIN.  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_ondisk  
  @SpecialOfferId int  
AS BEGIN  
  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  JOIN Sales.SpecialOffer_onDisk offer   
    ON s.SpecialOfferID = offer.SpecialOfferID   
    OR s.ProductID IN (SELECT ProductId FROM Sales.SpecialOfferProduct sop WHERE sop.SpecialOfferID = @SpecialOfferId)  
END  
```  
  
 Después de la conversión, el esquema de tabla y de procedimiento almacenado es el siguiente:  
  
```  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_Type AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesSpecialOffers_Type NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_TempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  recordcount int null  
  INDEX ix_fuzzySearchSalesSpecialOffers_TempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_inmem  
  @SpecialOfferId int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.FuzzySearchSalesSpecialOffers_Type  
  
  -- Find all special offers matching the conditions  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOffer_inmem offer   
    ON s.SpecialOfferID = offer.SpecialOfferID  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOfferProduct_inmem sop   
    ON sop.SpecialOfferId = @SpecialOfferId AND s.ProductID = sop.ProductId  
  
  -- Now we need to remove the duplicates from @matchingSpecialOffers  
  DECLARE @duplicates Sales.fuzzySearchSalesSpecialOffers_TempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, SpecialOfferid, recordcount)  
  SELECT SalesOrderId, SalesOrderDetailId, SpecialOfferId, COUNT(*)   
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId, SpecialOfferId  
  
  -- now there should be no duplicates within @duplicate  
  -- use @duplicate for join.  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates offer   
    ON    s.SalesOrderId = offer.SalesOrderId   
      AND s.SalesOrderDetailId = offer.SalesOrderDetailID   
      AND s.SpecialOfferId = offer.SpecialOfferId  
END  
GO  
```  
  
## <a name="side-effects"></a>Efectos secundarios  
 Si tiene más de un operador OR en la cláusula WHERE o la condición JOIN, el número de consultas que necesita ejecutar para simular el comportamiento puede aumentar exponencialmente. Esto puede ralentizar el rendimiento de las consultas y aumentar la utilización de memoria debido a la necesidad de usar variables de tabla optimizada para memoria.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
