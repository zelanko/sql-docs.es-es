---
title: Subconsultas (Azure SQL Data Warehouse, Almacenamiento de datos paralelos) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0e8ebd60-1936-48c9-b2b9-e099c8269fcf
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ab20f771fae4aa1ea5a31a11bc8c3e3f1e7c4ead
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33700744"
---
# <a name="subqueries-azure-sql-data-warehouse-parallel-data-warehouse"></a>Subconsultas (Azure SQL Data Warehouse, Almacenamiento de datos paralelos)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  En este tema se ofrecen ejemplos de uso de subconsultas en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 Para la instrucción SELECT, vea [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
## <a name="contents"></a>Contenido  
  
-   [Conceptos básicos](#Basics)  
  
-   [Ejemplos: SQL Data Warehouse y Almacenamiento de datos paralelos](#Examples)  
  
##  <a name="Basics"></a> Conceptos básicos  
 Subconsulta  
 Una subconsulta es una consulta anidada en una instrucción SELECT, INSERT, UPDATE o DELETE, o bien en otra subconsulta. Eso también se denomina consulta interna o selección interna.  
  
 Consulta externa  
 La instrucción que contiene la subconsulta. Esto también se denomina selección externa.  
  
 Subconsulta correlacionada  
 Una subconsulta que hace referencia a una tabla en la consulta externa.  
  
##  <a name="Examples"></a> Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En esta sección se proporcionan ejemplos de consultas admitidas en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="a-top-and-order-by-in-a-subquery"></a>A. TOP y ORDER BY en una subconsulta  
  
```  
SELECT * FROM tblA  
WHERE col1 IN  
    (SELECT TOP 100 col1 FROM tblB ORDER BY col1);  
  
```  
  
### <a name="b-having-clause-with-a-correlated-subquery"></a>B. Cláusula HAVING con una subconsulta correlacionada  
  
```  
SELECT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
GROUP BY dm.EmployeeKey, dm.FirstName, dm.LastName  
HAVING 5000 <=   
(SELECT sum(OrderQuantity)  
FROM FactResellerSales AS frs  
WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
  
```  
  
### <a name="c-correlated-subqueries-with-analytics"></a>C. Subconsultas correlacionadas con análisis  
  
```  
SELECT * FROM ReplA AS A   
WHERE A.ID IN   
    (SELECT sum(B.ID2) OVER() FROM ReplB AS B WHERE A.ID2 = B.ID);  
```  
  
### <a name="d-correlated-union-statements-in-a-subquery"></a>D. Instrucciones de unión correlacionadas en una subconsulta  
  
```  
SELECT * FROM RA   
WHERE EXISTS   
    (SELECT 1 FROM RB WHERE RB.b1 = RA.a1   
     UNION ALL SELECT 1 FROM RC);  
```  
  
### <a name="e-join-predicates-in-a-subquery"></a>E. Predicados de combinación en una subconsulta  
  
```  
SELECT * FROM RA INNER JOIN RB   
    ON RA.a1 = (SELECT COUNT(*) FROM RC);  
```  
  
### <a name="f-correlated-join-predicates-in-a-subquery"></a>F. Predicados de combinación correlacionados en una subconsulta  
  
```  
SELECT * FROM RA   
    WHERE RA.a2 IN   
    (SELECT 1 FROM RB INNER JOIN RC ON RA.a1=RB.b1+RC.c1);  
```  
  
### <a name="g-correlated-subselects-as-data-sources"></a>G. Subselecciones correlacionadas como orígenes de datos  
  
```  
SELECT * FROM RA   
    WHERE 3 = (SELECT COUNT(*)   
        FROM (SELECT b1 FROM RB WHERE RB.b1 = RA.a1) X);  
```  
  
### <a name="h-correlated-subqueries-in-the-data-values--used-with-aggregates"></a>H. Subconsultas correlacionadas en los valores de datos que se usan con agregados  
  
```  
SELECT Rb.b1, (SELECT RA.a1 FROM RA WHERE RB.b1 = RA.a1) FROM RB GROUP BY RB.b1;  
```  
  
### <a name="i-using-in-with-a-correlated-subquery"></a>I. Uso de IN con una subconsulta correlacionada  
 En el siguiente ejemplo se utiliza `IN` en una subconsulta correlativa o repetitiva. Se trata de una consulta que depende de la consulta externa de sus valores. La consulta interna se ejecuta varias veces, una por cada fila que pueda seleccionar la consulta externa. Esta consulta recupera una instancia de la `EmployeeKey` junto al nombre y apellido de cada empleado para el que `OrderQuantity` en la tabla `FactResellerSales` sea `5` y cuyos números de identificación coincidan en las tablas `DimEmployee` y `FactResellerSales`.  
  
```  
SELECT DISTINCT dm.EmployeeKey, dm.FirstName, dm.LastName   
FROM DimEmployee AS dm   
WHERE 5 IN   
    (SELECT OrderQuantity  
    FROM FactResellerSales AS frs  
    WHERE dm.EmployeeKey = frs.EmployeeKey)  
ORDER BY EmployeeKey;  
```  
  
### <a name="j-using-exists-versus-in-with-a-subquery"></a>J. Uso de EXISTS frente a IN con una subconsulta  
 En el ejemplo siguiente se muestran consultas que son semánticamente equivalentes para demostrar la diferencia entre el uso de la palabra clave `EXISTS` y la palabra clave `IN`. Ambos son ejemplos de una subconsulta que recupera una instancia de cada nombre de producto cuya subcategoría de producto es `Road Bikes`. `ProductSubcategoryKey` coincide entre las tablas `DimProduct` y `DimProductSubcategory`.  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE EXISTS  
    (SELECT *  
     FROM DimProductSubcategory AS dps   
     WHERE dp.ProductSubcategoryKey = dps.ProductSubcategoryKey  
           AND dps.EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
 o bien  
  
```  
SELECT DISTINCT EnglishProductName  
FROM DimProduct AS dp   
WHERE dp.ProductSubcategoryKey IN  
    (SELECT ProductSubcategoryKey  
     FROM DimProductSubcategory   
     WHERE EnglishProductSubcategoryName = 'Road Bikes')  
ORDER BY EnglishProductName;  
```  
  
### <a name="k-using-multiple-correlated-subqueries"></a>K. Uso de varias subconsultas correlacionadas  
 En este ejemplo se utilizan dos subconsultas correlativas para buscar los nombres de los empleados que han vendido un producto específico.  
  
```  
SELECT DISTINCT LastName, FirstName, e.EmployeeKey  
FROM DimEmployee e JOIN FactResellerSales s ON e.EmployeeKey = s.EmployeeKey  
WHERE ProductKey IN  
(SELECT ProductKey FROM DimProduct WHERE ProductSubcategoryKey IN  
(SELECT ProductSubcategoryKey FROM DimProductSubcategory   
 WHERE EnglishProductSubcategoryName LIKE '%Bikes'))  
ORDER BY LastName  
;  
  
```  
  
  
