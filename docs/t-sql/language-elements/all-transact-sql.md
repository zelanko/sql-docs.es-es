---
title: TODOS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- ALL_TSQL
- ALL
dev_langs:
- TSQL
helpviewer_keywords:
- single-column set of values [SQL Server]
- ALL (Transact-SQL)
ms.assetid: 4b0c002e-1ffd-4425-a980-11fdc1f24af7
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1fd1b250a30b83a3b014384aafee6c40ff4f1a5a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="all-transact-sql"></a>ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compara un valor escalar con un conjunto de valores de una sola columna.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
scalar_expression { = | <> | != | > | >= | !> | < | <= | !< } ALL ( subquery )  
```  
  
## <a name="arguments"></a>Argumentos  
 *scalar_expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 Es un operador de comparación.  
  
 *subconsulta*  
 Es una subconsulta que devuelve un conjunto de resultados de una columna. El tipo de datos de la columna devuelta debe ser el mismo tipo de datos que el tipo de datos de *scalar_expression*.  
  
 Es una instrucción SELECT restringida en la que no se permiten la cláusula ORDER BY ni la palabra clave INTO.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor de resultado  
 Devuelve TRUE cuando la comparación especificada es TRUE para todos los pares (*scalar_expression***,***x)*, cuando *x* es un valor en el conjunto de columna única; de lo contrario, devuelve FALSE.  
  
## <a name="remarks"></a>Comentarios  
 Requiere que todos los *scalar_expression* a compare de forma positiva con cada valor devuelto por la subconsulta. Por ejemplo, si la subconsulta devuelve los valores 2 y 3, *scalar_expression* < = ALL (subconsulta) se evaluaría como TRUE para un *scalar_expression* de 2. Si la subconsulta devuelve los valores 2 y 3, *scalar_expression* = ALL (subconsulta) se evaluaría como FALSE, porque algunos de los valores de la subconsulta (el valor de 3) no cumpliría los criterios de la expresión.  
  
 Para instrucciones que requieren la *scalar_expression* para comparar de forma positiva a solo un valor devuelto por la subconsulta, vea [algunos &#124; CUALQUIER &#40; Transact-SQL &#41; ](../../t-sql/language-elements/some-any-transact-sql.md).  
  
 Este tema hace referencia a ALL cuando se utiliza con una subconsulta. También puede utilizar con [UNION](../../t-sql/language-elements/set-operators-union-transact-sql.md) y [seleccione](../../t-sql/queries/select-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea un procedimiento almacenado que determina si todos los componentes de un determinado `SalesOrderID` en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos se puede fabricar en el número de días especificado. En el ejemplo se usa una subconsulta para crear una lista del número del valor de `DaysToManufacture` para todos los componentes del `SalesOrderID` específico y, a continuación, confirma que todos los `DaysToManufacture` están dentro del número de días especificado.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE DaysToBuild @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays >= ALL  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'All items for this order can be manufactured in specified number of days or less.'  
ELSE   
PRINT 'Some items for this order cannot be manufactured in specified number of days or less.' ;  
  
```  
  
 Para probar el procedimiento, ejecútelo con `SalesOrderID 49080`, que tiene un componente que requiere `2` días y dos componentes que requieren 0 días. La primera instrucción siguiente cumple los criterios. La segunda consulta no los cumple.  
  
```  
EXECUTE DaysToBuild 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in specified number of days or less.`  
  
```  
EXECUTE DaysToBuild 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Some items for this order cannot be manufactured in specified number of days or less.`  
  
## <a name="see-also"></a>Vea también  
 [CASO &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40; Transact-SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

