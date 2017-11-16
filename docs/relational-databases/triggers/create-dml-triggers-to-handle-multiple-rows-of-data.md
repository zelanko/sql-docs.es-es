---
title: "Creación de desencadenadores DML para administrar varias filas de datos | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multiple row DML triggers
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- multirow DML triggers [SQL Server]
- INSERT statement [SQL Server], DML triggers
- DML triggers, multirow
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 55a772a063a33749af39f43d6a070bfdf8216796
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="create-dml-triggers-to-handle-multiple-rows-of-data"></a>Crear desencadenadores DML para administrar varias filas de datos
  Cuando escriba el código para un desencadenador DML, tenga en cuenta que la instrucción que hace que se active el disparador puede ser una sola instrucción que afecte a varias filas de datos, en lugar de una sola fila. Este comportamiento es habitual para los desencadenadores UPDATE y DELETE, ya que estas instrucciones suelen afectar a varias filas. No es tan corriente para los desencadenadores INSERT, porque la instrucción INSERT básica solo agrega una fila. Pero, dado que un desencadenador INSERT puede ser activado por una instrucción INSERT INTO (*nombre_tabla*) SELECT, la inserción de muchas filas puede tener como resultado la invocación de un solo desencadenador.  
  
 Las consideraciones acerca de los procesos que afectan a varias filas son especialmente importantes cuando la función de un desencadenador DML consiste en volver a calcular automáticamente los valores de resumen de una tabla y almacenar los resultados en otra para realizar cálculos continuos.  
  
> [!NOTE]  
>  No se recomienda utilizar cursores en desencadenadores, ya que pueden reducir el rendimiento. Para diseñar un desencadenador que afecte a varias filas, utilice la lógica basada en conjuntos de filas, en lugar de cursores.  
  
## <a name="examples"></a>Ejemplos  
 Los desencadenadores DML descritos en los ejemplos siguientes están diseñados para almacenar el total acumulativo de una columna en otra tabla de la base de datos de muestra [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
### <a name="a-storing-a-running-total-for-a-single-row-insert"></a>A. Almacenar un total acumulativo para una inserción de una sola fila  
 La primera versión del desencadenador DML funcionará correctamente para la inserción de una fila cuando se cargue una fila de datos en la tabla `PurchaseOrderDetail` . El desencadenador DML se activa mediante una instrucción INSERT y la nueva fila se carga en la tabla **inserted** mientras dure la ejecución del desencadenador. La instrucción `UPDATE` lee el valor de la columna `LineTotal` para la fila y lo agrega al valor existente en la columna `SubTotal` de la tabla `PurchaseOrderHeader` . La cláusula `WHERE` garantiza que la fila actualizada de la tabla `PurchaseOrderDetail` coincida con el `PurchaseOrderID` de la fila de la tabla **inserted** .  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### <a name="b-storing-a-running-total-for-a-multirow-or-single-row-insert"></a>B. Almacenar un total acumulativo para una inserción de una o varias filas  
 En caso de una inserción de varias filas, el desencadenador DML del ejemplo A no funcionaría correctamente; la expresión situada a la derecha de una asignación de una instrucción UPDATE (`SubTotal` + `LineTotal`) debe tener un solo valor, no una lista de valores. Por lo tanto, el efecto del desencadenador es recuperar un valor de una sola fila de la tabla **inserted** y agregarlo al valor `SubTotal` existente en la tabla `PurchaseOrderHeader` para un valor `PurchaseOrderID` específico. Esta operación puede no tener el efecto esperado si se da un solo valor `PurchaseOrderID` más de una vez en la tabla **inserted** .  
  
 Para actualizar correctamente la tabla `PurchaseOrderHeader` , el desencadenador debe permitir que pueda haber varias filas en la tabla **inserted** . Puede hacerlo utilizando la función `SUM` que calcula el total `LineTotal` para un grupo de filas de la tabla **inserted** para cada `PurchaseOrderID`. La función `SUM` se incluye en una subconsulta correlacionada (la instrucción `SELECT` entre paréntesis). Esta subconsulta devuelve un único valor para cada `PurchaseOrderID` de la tabla **inserted** que coincida o esté correlacionado con un `PurchaseOrderID` de la tabla `PurchaseOrderHeader` .  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 Este desencadenador también funciona correctamente para la inserción de una sola fila; la suma de los valores de la columna `LineTotal` corresponde a la suma de una sola fila. Sin embargo, con este desencadenador la subconsulta correlacionada y el operador `IN` que se utiliza en la cláusula `WHERE` requieren un procesamiento adicional por parte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto no es necesario para una inserción de una sola fila.  
  
### <a name="c-storing-a-running-total-based-on-the-type-of-insert"></a>C. Almacenar un total acumulativo basado en el tipo de inserción  
 Puede cambiar el desencadenador a fin de utilizar el método óptimo para el número de filas. Por ejemplo, es posible utilizar la función `@@ROWCOUNT` en la lógica del desencadenador para que distinga entre la inserción de una fila y la de varias filas.  
  
```  
-- Trigger valid for multirow and single row inserts  
-- and optimal for single row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail3  
ON Purchasing.PurchaseOrderDetail  
FOR INSERT AS  
IF @@ROWCOUNT = 1  
BEGIN  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
END  
ELSE  
BEGIN  
      UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted)  
END;  
```  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores DML](../../relational-databases/triggers/dml-triggers.md)  
  
  
