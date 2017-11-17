---
title: ALGUNOS | CUALQUIER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
f1_keywords:
- SOME
- SOME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- scalar values
- comparing scalar with single-column set
- ANY operator
- SOME | ANY keyword
- single-column set of values [SQL Server]
ms.assetid: 1f717ad6-f67b-4980-9397-577ecb0e5789
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a67801d62cb05cdb0b589548e8bd3f9676d5840a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="some--any-transact-sql"></a>SOME | ANY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compara un valor escalar con un conjunto de valores de una sola columna. SOME y ANY son equivalentes.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
scalar_expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
     { SOME | ANY } ( subquery )   
```  
  
## <a name="arguments"></a>Argumentos  
 *scalar_expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 { = | <> | != | > | >= | !> | < | <= | !< }  
 Es cualquier operador de comparación válido.  
  
 SOME | ANY  
 Especifica que se debe realizar una comparación.  
  
 *subconsulta*  
 Es una subconsulta que tiene un conjunto de resultados de una columna. El tipo de datos de la columna devuelta debe ser el mismo tipo de datos que *scalar_expression*.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor de resultado  
 SOME o ANY devuelven **TRUE** cuando la comparación especificada es TRUE para cualquier par (*scalar_expression***,***x*) donde *x* es un valor en el conjunto de una sola columna; en caso contrario, devuelve **FALSE**.  
  
## <a name="remarks"></a>Comentarios  
 SOME requiere la *scalar_expression* a compare de forma positiva con al menos un valor devuelto por la subconsulta. Para instrucciones que requieren la *scalar_expression* para comparar de forma positiva con cada valor devuelto por la subconsulta, vea [todos &#40; Transact-SQL &#41; ](../../t-sql/language-elements/all-transact-sql.md). Por ejemplo, si la subconsulta devuelve los valores 2 y 3, *scalar_expression* = SOME (subconsulta) se evaluaría como TRUE para un *scalar_express* de 2. Si la subconsulta devuelve los valores 2 y 3, *scalar_expression* = ALL (subconsulta) se evaluaría como FALSE, porque algunos de los valores de la subconsulta (el valor de 3) no cumpliría los criterios de la expresión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-running-a-simple-example"></a>A. Ejecutar un ejemplo sencillo  
 Las instrucciones siguientes crean una tabla simple y agregan los valores `1`, `2`, `3` y `4` a la columna de `ID`.  
  
```  
CREATE TABLE T1  
(ID int) ;  
GO  
INSERT T1 VALUES (1) ;  
INSERT T1 VALUES (2) ;  
INSERT T1 VALUES (3) ;  
INSERT T1 VALUES (4) ;  
```  
  
 La consulta siguiente devuelve `TRUE` porque `3` es menor que alguno de los valores de la tabla.  
  
```  
IF 3 < SOME (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
 La consulta siguiente devuelve `FALSE` porque `3` no es menor que todos los valores de la tabla.  
  
```  
IF 3 < ALL (SELECT ID FROM T1)  
PRINT 'TRUE'   
ELSE  
PRINT 'FALSE' ;  
```  
  
### <a name="b-running-a-practical-example"></a>B. Ejecutar un ejemplo práctico  
 En el ejemplo siguiente se crea un procedimiento almacenado que determina si todos los componentes de un determinado `SalesOrderID` en el `AdventureWorks2012` base de datos se puede fabricar en el número de días especificado. En el ejemplo se usa una subconsulta para crear una lista de valores de `DaysToManufacture` para todos los componentes del `SalesOrderID` especificado y, a continuación, se comprueba si alguno de los valores devueltos por la subconsulta es mayor que el número de días especificado. Si cada valor de `DaysToManufacture` que se devuelve es menor que el número proporcionado, la condición es TRUE y se imprime el primer mensaje.  
  
```  
-- Uses AdventureWorks  
  
CREATE PROCEDURE ManyDaysToComplete @OrderID int, @NumberOfDays int  
AS  
IF   
@NumberOfDays < SOME  
   (  
    SELECT DaysToManufacture  
    FROM Sales.SalesOrderDetail  
    JOIN Production.Product   
    ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID   
    WHERE SalesOrderID = @OrderID  
   )  
PRINT 'At least one item for this order cannot be manufactured in specified number of days.'  
ELSE   
PRINT 'All items for this order can be manufactured in the specified number of days or less.' ;  
  
```  
  
 Para probar el procedimiento, ejecute el procedimiento mediante el uso de la `SalesOrderID``49080`, que tiene un componente que requiere `2` días y dos componentes que requieren 0 días. La primera instrucción cumple los criterios. La segunda consulta no los cumple.  
  
```  
EXECUTE ManyDaysToComplete 49080, 2 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `All items for this order can be manufactured in the specified number of days or less.`  
  
```  
EXECUTE ManyDaysToComplete 49080, 1 ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `At least one item for this order cannot be manufactured in specified number of days.`  
  
## <a name="see-also"></a>Vea también  
 [Todas las &#40; Transact-SQL &#41;](../../t-sql/language-elements/all-transact-sql.md)   
 [CASO &#40; Transact-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [IN &#40; Transact-SQL &#41;](../../t-sql/language-elements/in-transact-sql.md)  
  
  

