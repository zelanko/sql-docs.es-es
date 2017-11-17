---
title: UNION (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UNION
- UNION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UNION queries
- combining query results
- UNION operator [SQL Server]
ms.assetid: 607c296f-8a6a-49bc-975a-b8d0c0914df7
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 29f86913fd2fb6bf04c4c00d95427d34128c8fee
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-operators---union-transact-sql"></a>Operadores - de conjuntos UNION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Combina los resultados de dos o más consultas en un solo conjunto de resultados que incluye todas las filas que pertenecen a las consultas de la unión. La operación UNION es distinta de la utilización de combinaciones de columnas de dos tablas.  
  
 A continuación se muestran las reglas básicas para combinar los conjuntos de resultados de dos consultas con UNION:  
  
-   El número y el orden de las columnas debe ser el mismo en todas las consultas.  
  
-   Los tipos de datos deben ser compatibles.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
    { <query_specification> | ( <query_expression> ) }   
  UNION [ ALL ]   
  <query_specification | ( <query_expression> )   
 [ UNION [ ALL ] <query_specification> | ( <query_expression> )   
    [ ...n ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
\<query_specification > | ( \<query_expression >) es una especificación de consulta o expresión de consulta que devuelve datos que se combinarán con los datos de otra consulta especificación o expresión de consulta. No es preciso que las definiciones de las columnas que forman parte de una operación UNION sean iguales, pero deben ser compatibles a través de una conversión implícita. Cuando los tipos de datos difieren, el tipo de datos resultante se determina según las reglas de [prioridad de tipo de datos](../../t-sql/data-types/data-type-precedence-transact-sql.md). Cuando los tipos son los mismos pero varían en cuanto a precisión, escala o longitud, el resultado se determina según las mismas reglas para combinar expresiones. Para más información, vea [Precisión, escala y longitud &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 Columnas de la **xml** tipo de datos debe ser equivalente. Todas las columnas deben tener un tipo de esquema XML o no tener tipo. Si tienen tipo, debe ser el de la misma colección de esquemas XML.  
  
 UNION  
 Especifica que se deben combinar varios conjuntos de resultados para ser devueltos como un solo conjunto de resultados.  
  
 ALL  
 Agrega todas las filas a los resultados. Incluye las filas duplicadas. Si no se especifica, las filas duplicadas se quitan.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-a-simple-union"></a>A. Usar una instrucción UNION simple  
 En el ejemplo siguiente, el conjunto de resultados incluye el contenido de las columnas `ProductModelID` y `Name` de las tablas `ProductModel` y `Gloves`.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Here is the simple union.  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
```  
  
### <a name="b-using-select-into-with-union"></a>B. Usar SELECT INTO con UNION  
 En el ejemplo siguiente, la cláusula `INTO` de la segunda instrucción `SELECT` especifica que la tabla denominada `ProductResults` contiene el conjunto final de resultados de la unión de las columnas designadas de las tablas `ProductModel` y `Gloves`. Tenga en cuenta que la tabla `Gloves` se crea en la primera instrucción `SELECT`.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.ProductResults', 'U') IS NOT NULL  
DROP TABLE dbo.ProductResults;  
GO  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
INTO dbo.ProductResults  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
SELECT ProductModelID, Name   
FROM dbo.ProductResults;  
  
```  
  
### <a name="c-using-union-of-two-select-statements-with-order-by"></a>C. Usar UNION con dos instrucciones SELECT y ORDER BY  
 El orden de algunos parámetros empleados con la cláusula UNION es importante. En el ejemplo siguiente se muestra el uso correcto e incorrecto de `UNION` en dos instrucciones `SELECT` en las que se va a cambiar el nombre de una columna en el resultado.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.Gloves', 'U') IS NOT NULL  
DROP TABLE dbo.Gloves;  
GO  
-- Create Gloves table.  
SELECT ProductModelID, Name  
INTO dbo.Gloves  
FROM Production.ProductModel  
WHERE ProductModelID IN (3, 4);  
GO  
  
/* INCORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
ORDER BY Name  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves;  
GO  
  
/* CORRECT */  
-- Uses AdventureWorks  
  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID NOT IN (3, 4)  
UNION  
SELECT ProductModelID, Name  
FROM dbo.Gloves  
ORDER BY Name;  
GO  
  
```  
  
### <a name="d-using-union-of-three-select-statements-to-show-the-effects-of-all-and-parentheses"></a>D. Usar UNION de tres instrucciones SELECT para mostrar los efectos de ALL y los paréntesis  
 En los siguientes ejemplos se utiliza `UNION` para combinar los resultados de tres tablas que tienen las mismas 5 filas de datos. En el primer ejemplo se utiliza `UNION ALL` para mostrar los registros duplicados y se devuelven las 15 filas. En el segundo ejemplo se utiliza `UNION` sin `ALL` para eliminar las filas duplicadas de los resultados combinados de las tres instrucciones `SELECT` y se devuelven 5 filas.  
  
 En el tercer ejemplo se utiliza `ALL` con el primer `UNION` y los paréntesis incluyen al segundo `UNION` que no utiliza `ALL`. El segundo `UNION` se procesa en primer lugar porque se encuentra entre paréntesis. Devuelve 5 filas porque no se utiliza la opción `ALL` y se quitan los duplicados. Estas 5 filas se combinan con los resultados del primer `SELECT` mediante las palabras clave `UNION ALL`. Esto no quita los duplicados entre los dos conjuntos de 5 filas. El resultado final es de 10 filas.  
  
```  
-- Uses AdventureWorks  
  
IF OBJECT_ID ('dbo.EmployeeOne', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeOne;  
GO  
IF OBJECT_ID ('dbo.EmployeeTwo', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeTwo;  
GO  
IF OBJECT_ID ('dbo.EmployeeThree', 'U') IS NOT NULL  
DROP TABLE dbo.EmployeeThree;  
GO  
  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeOne  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeTwo  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
SELECT pp.LastName, pp.FirstName, e.JobTitle   
INTO dbo.EmployeeThree  
FROM Person.Person AS pp JOIN HumanResources.Employee AS e  
ON e.BusinessEntityID = pp.BusinessEntityID  
WHERE LastName = 'Johnson';  
GO  
-- Union ALL  
SELECT LastName, FirstName, JobTitle  
FROM dbo.EmployeeOne  
UNION ALL  
SELECT LastName, FirstName ,JobTitle  
FROM dbo.EmployeeTwo  
UNION ALL  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle  
FROM dbo.EmployeeOne  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION   
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree;  
GO  
  
SELECT LastName, FirstName,JobTitle   
FROM dbo.EmployeeOne  
UNION ALL  
(  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeTwo  
UNION  
SELECT LastName, FirstName, JobTitle   
FROM dbo.EmployeeThree  
);  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-a-simple-union"></a>E. Usar una instrucción UNION simple  
 En el ejemplo siguiente, el conjunto de resultados incluye el contenido de la `CustomerKey` columnas de ambos el `FactInternetSales` y `DimCustomer` tablas. Puesto que no se usa la palabra clave ALL, los duplicados se excluyen de los resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="f-using-union-of-two-select-statements-with-order-by"></a>F. Usar UNION con dos instrucciones SELECT y ORDER BY  
 Cuando una instrucción SELECT en una instrucción UNION incluye una cláusula ORDER BY, se debe colocar esa cláusula después de todas las instrucciones SELECT. En el ejemplo siguiente se muestra el uso correcto e incorrecto de `UNION` en dos `SELECT` las instrucciones en el que se ordena una columna con ORDER BY.  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT  
SELECT CustomerKey   
FROM FactInternetSales    
ORDER BY CustomerKey  
UNION   
SELECT CustomerKey   
FROM DimCustomer  
ORDER BY CustomerKey;  
  
-- CORRECT   
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales    
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="g-using-union-of-two-select-statements-with-where-and-order-by"></a>G. Mediante la unión de dos instrucciones SELECT con WHERE y ORDER BY  
 En el ejemplo siguiente se muestra el uso correcto e incorrecto de `UNION` en dos `SELECT` instrucciones donde donde y son necesarias ORDER BY.  
  
```  
-- Uses AdventureWorks  
  
-- INCORRECT   
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
ORDER BY CustomerKey   
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
  
-- CORRECT  
USE AdventureWorksPDW2012;  
  
SELECT CustomerKey   
FROM FactInternetSales   
WHERE CustomerKey >= 11000  
UNION   
SELECT CustomerKey   
FROM DimCustomer   
ORDER BY CustomerKey;  
```  
  
### <a name="h-using-union-of-three-select-statements-to-show-effects-of-all-and-parentheses"></a>H. Utilizar UNION de tres instrucciones SELECT para mostrar los efectos de ALL y los paréntesis  
 Los ejemplos siguientes usan `UNION` para combinar los resultados de **la misma tabla** para mostrar los efectos de ALL y los paréntesis al usar `UNION`.  
  
 El primer ejemplo se utiliza `UNION ALL` para mostrar duplicado registros y devuelve cada fila de la tabla de origen tres veces. El segundo ejemplo usa `UNION` sin `ALL` para eliminar las filas duplicadas de los resultados combinados de las tres `SELECT` instrucciones y devuelve solo las filas sin duplicar la tabla de origen.  
  
 El tercer ejemplo se utiliza `ALL` con la primera `UNION` y el segundo entre paréntesis `UNION` que está usando no `ALL`. El segundo `UNION` se procesa en primer lugar porque está entre paréntesis. Devuelve solo las filas sin duplicar de la tabla porque el `ALL` no se utiliza la opción y se quitan los duplicados. Estas filas se combinan con los resultados de la primera `SELECT` utilizando el `UNION ALL` palabras clave. Esto no quita los duplicados entre los dos conjuntos.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer;  
  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION ALL  
(  
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
UNION   
SELECT CustomerKey, FirstName, LastName  
FROM DimCustomer  
);  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Ejemplos SELECT &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
  
  


