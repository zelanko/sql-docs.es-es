---
title: IN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/29/2016
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
- IN_TSQL
- IN
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], matching
- NOT IN keyword
- 8623 (Database Engine error)
- matching values in subquery or list [SQL Server]
- IN keyword
- 8632 (Database Engine error)
ms.assetid: 4419de73-96b1-4dfe-8500-f4507915db04
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70b186107966791e29ccb76ea9c310724b76e3b6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="in-transact-sql"></a>IN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Determina si un valor especificado coincide con algún valor de una subconsulta o una lista.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
test_expression [ NOT ] IN   
    ( subquery | expression [ ,...n ]  
    )   
```  
  
## <a name="arguments"></a>Argumentos  
 *test_expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 *subconsulta*  
 Es una subconsulta que tiene un conjunto de resultados de una columna. Esta columna debe tener los mismos datos de tipo como *test_expression*.  
  
 *expresión*[ **,**... *n* ]  
 Es una lista de expresiones en la que se buscará una coincidencia. Todas las expresiones deben ser del mismo tipo como *test_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor de resultado  
 Si el valor de *test_expression* es igual a cualquier valor devuelto por *subconsulta* o es igual a cualquier *expresión* en la lista separada por comas, el valor del resultado es TRUE. en caso contrario, el valor del resultado es FALSE.  
  
 El uso de NOT IN niega el *subconsulta* valor o *expresión*.  
  
> [!CAUTION]  
>  Los valores devueltos por null *subconsulta* o *expresión* que se comparan con *test_expression* mediante IN o NOT IN devuelven UNKNOWN. La utilización de valores NULL con IN o NOT IN puede provocar resultados inesperados.  
  
## <a name="remarks"></a>Comentarios  
 Se incluyen explícitamente un gran número de valores (muchos miles de valores separados por comas) entre paréntesis, en una cláusula IN puede consumir recursos y devolver errores 8623 o 8632. Para solucionar este problema, almacene los elementos de la lista IN en una tabla y usar una subconsulta SELECT dentro de una cláusula IN.  
  
 Error 8623:  
  
 `The query processor ran out of internal resources and could not produce a query plan. This is a rare event and only expected for extremely complex queries or queries that reference a very large number of tables or partitions. Please simplify the query. If you believe you have received this message in error, contact Customer Support Services for more information.`  
  
 Error 8632:  
  
 `Internal error: An expression services limit has been reached. Please look for potentially complex expressions in your query, and try to simplify them.`  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-comparing-or-and-in"></a>A. Comparar OR e IN  
 En el ejemplo siguiente se selecciona una lista con los nombres de los empleados que son ingenieros de diseño, ingenieros de herramientas o asistentes de marketing.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle = 'Design Engineer'   
   OR e.JobTitle = 'Tool Designer'   
   OR e.JobTitle = 'Marketing Assistant';  
GO  
```  
  
 No obstante, con IN se recuperan los mismos resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, e.JobTitle  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e  
    ON p.BusinessEntityID = e.BusinessEntityID  
WHERE e.JobTitle IN ('Design Engineer', 'Tool Designer', 'Marketing Assistant');  
GO  
```  
  
 Éste es el conjunto de resultados que se obtiene con cualquiera de las dos consultas.  
  
```  
FirstName   LastName      Title  
---------   ---------   ---------------------  
Sharon      Salavaria   Design Engineer                                     
Gail        Erickson    Design Engineer                                     
Jossef      Goldberg    Design Engineer                                     
Janice      Galvin      Tool Designer                                       
Thierry     D'Hers      Tool Designer                                       
Wanida      Benshoof    Marketing Assistant                                 
Kevin       Brown       Marketing Assistant                                 
Mary        Dempsey     Marketing Assistant                                 
  
(8 row(s) affected)  
```  
  
### <a name="b-using-in-with-a-subquery"></a>B. Utilizar IN con una subconsulta  
 En el ejemplo siguiente se buscan todos los identificadores de vendedor de la tabla `SalesPerson` para los empleados cuya cuota de ventas sea superior a 250.000 dólares al año y, después, se seleccionan en la tabla `Employee` los nombres de todos los empleados cuyo `EmployeeID` coincida con los resultados de la subconsulta `SELECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName   LastName                                             
---------   --------   
Tsvi         Reiter                                              
Michael      Blythe                                              
Tete         Mensa-Annan                                         
  
(3 row(s) affected)  
```  
  
### <a name="c-using-not-in-with-a-subquery"></a>C. Utilizar NOT IN con una subconsulta  
 En el ejemplo siguiente se buscan los vendedores con una cuota inferior a 250.000 dólares. `NOT IN` busca los vendedores que no coinciden con los elementos de la lista de valores.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName  
FROM Person.Person AS p  
    JOIN Sales.SalesPerson AS sp  
    ON p.BusinessEntityID = sp.BusinessEntityID  
WHERE p.BusinessEntityID NOT IN  
   (SELECT BusinessEntityID  
   FROM Sales.SalesPerson  
   WHERE SalesQuota > 250000);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-in-and-not-in"></a>D. Uso de entrada y no en  
 En el ejemplo siguiente se buscan todas las entradas de la `FactInternetSales` que coincidan con la tabla `SalesReasonKey` valores en el `DimSalesReason` tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
IN (SELECT SalesReasonKey FROM DimSalesReason);   
```  
  
 En el ejemplo siguiente se buscan todas las entradas de la `FactInternetSalesReason` tabla que no coinciden con `SalesReasonKey` valores en el `DimSalesReason` tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT * FROM FactInternetSalesReason   
WHERE SalesReasonKey   
NOT IN (SELECT SalesReasonKey FROM DimSalesReason);  
```  
  
### <a name="e-using-in-with-an-expression-list"></a>E. Usar con una lista de expresiones  
 En el ejemplo siguiente se busca todos los identificadores para los vendedores de la `DimEmployee` de la tabla para los empleados que tienen un primer nombre que es una `Mike` o `Michael`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM DimEmployee  
WHERE FirstName IN ('Mike', 'Michael');  
```  
  
## <a name="see-also"></a>Vea también  
 [CASO &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [Todas las &#40; Transact-SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [Algunos &#124; CUALQUIER &#40; Transact-SQL &#41;](../../t-sql/language-elements/some-any-transact-sql.md)  
  
  




