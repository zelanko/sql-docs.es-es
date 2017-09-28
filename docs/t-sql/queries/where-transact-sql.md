---
title: DONDE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WHERE_TSQL
- WHERE
dev_langs:
- TSQL
helpviewer_keywords:
- retrieving rows
- clauses [SQL Server], WHERE
- WHERE clause, about WHERE clause
- row retrieval [SQL Server], WHERE clause
- WHERE clause
ms.assetid: a8430421-7bce-4fab-a2d2-56c00a3c6fa4
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5835510f37f52d57d2c23918a30dde10e7496a5d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="where-transact-sql"></a>WHERE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica la condición de búsqueda de las filas devueltas por la consulta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
[ WHERE <search_condition> ]  
```  
  
## <a name="arguments"></a>Argumentos  
\<*search_condition* > define la condición que debe cumplirse para que se devuelvan las filas. No hay límite en el número de predicados que se pueden incluir en una condición de búsqueda. Para obtener más información sobre predicados y las condiciones de búsqueda, vea [condición de búsqueda &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra cómo utilizar algunas condiciones de búsqueda comunes en la cláusula `WHERE`.  
  
### <a name="a-finding-a-row-by-using-a-simple-equality"></a>A. Buscar una fila utilizando una igualdad simple  
  
```  
USE AdventureWorks2012  
GO  
SELECT ProductID, Name  
FROM Production.Product  
WHERE Name = 'Blade' ;  
GO  
```  
  
### <a name="b-finding-rows-that-contain-a-value-as-a-part-of-a-string"></a>B. Buscar las filas que contienen un valor como una parte de una cadena  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name LIKE ('%Frame%');  
GO  
```  
  
### <a name="c-finding-rows-by-using-a-comparison-operator"></a>C. Buscar filas utilizando un operador de comparación  
  
```  
SELECT ProductID, Name  
FROM Production.Product  
WHERE ProductID <= 12 ;  
GO  
```  
  
### <a name="d-finding-rows-that-meet-any-of-three-conditions"></a>D. Buscar las filas que cumplen alguna de tres condiciones  
  
```  
SELECT ProductID, Name  
FROM Production.Product  
WHERE ProductID = 2  
OR ProductID = 4   
OR Name = 'Spokes' ;  
GO  
```  
  
### <a name="e-finding-rows-that-must-meet-several-conditions"></a>E. Buscar las filas que deben cumplir varias condiciones  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name LIKE ('%Frame%')  
AND Name LIKE ('HL%')  
AND Color = 'Red' ;  
GO  
```  
  
### <a name="f-finding-rows-that-are-in-a-list-of-values"></a>F. Buscar las filas que están en una lista de valores  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE Name IN ('Blade', 'Crown Race', 'Spokes');  
GO  
```  
  
### <a name="g-finding-rows-that-have-a-value-between-two-values"></a>G. Buscar las filas que tienen un valor comprendido entre dos valores  
  
```  
SELECT ProductID, Name, Color  
FROM Production.Product  
WHERE ProductID BETWEEN 725 AND 734;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En los ejemplos siguientes se muestra cómo utilizar algunas condiciones de búsqueda comunes en la cláusula `WHERE`.  
  
### <a name="h-finding-a-row-by-using-a-simple-equality"></a>H. Buscar una fila utilizando una igualdad simple  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName = 'Smith' ;  
```  
  
### <a name="i-finding-rows-that-contain-a-value-as-part-of-a-string"></a>I. Buscar las filas que contienen un valor como parte de una cadena  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE ('%Smi%');  
```  
  
### <a name="j-finding-rows-by-using-a-comparison-operator"></a>J. Buscar filas utilizando un operador de comparación  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey  <= 500;  
```  
  
### <a name="k-finding-rows-that-meet-any-of-three-conditions"></a>K. Buscar las filas que cumplen alguna de tres condiciones  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey = 1 OR EmployeeKey = 8 OR EmployeeKey = 12;  
```  
  
### <a name="l-finding-rows-that-must-meet-several-conditions"></a>L. Buscar las filas que deben cumplir varias condiciones  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey <= 500 AND LastName LIKE '%Smi%' AND FirstName LIKE '%A%';  
```  
  
### <a name="m-finding-rows-that-are-in-a-list-of-values"></a>M. Buscar las filas que están en una lista de valores  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName IN ('Smith', 'Godfrey', 'Johnson');  
```  
  
### <a name="n-finding-rows-that-have-a-value-between-two-values"></a>N. Buscar las filas que tienen un valor comprendido entre dos valores  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey Between 100 AND 200;  
```  
  
## <a name="see-also"></a>Vea también  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Predicados &#40; Transact-SQL &#41;](~/t-sql/queries/predicates.md)   
 [Condición de búsqueda &#40; Transact-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
  



