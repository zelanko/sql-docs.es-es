---
title: VAR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- VAR
- VAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statistical variances
- expressions [SQL Server], statistical variance
- VAR function [Transact-SQL]
ms.assetid: 71dfc339-16c8-42f9-8555-ad45400f7f9b
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 677b8eae4863b18d5e94e8c7f577d13ebfe01031
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="var-transact-sql"></a>VAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la varianza estadística de todos los valores de la expresión especificada. Puede ir seguido por el [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
VAR ( [ ALL | DISTINCT ] expression )   
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Aggregate Function Syntax   
VAR ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
VAR (expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>Argumentos  
 **ALL**  
 Aplica la función a todos los valores. ALL es el valor predeterminado.  
  
 DISTINCT  
 Especifica que se tiene en cuenta cada valor único.  
  
 *expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de exactos categoría de tipos de datos numéricos o numéricos aproximados excepto para la **bits** tipo de datos. No se permiten funciones de agregado ni subconsultas.  
  
 SOBRE **(** [ *partition_by_clause* ] *order_by_clause***)**  
 *partition_by_clause* divide el conjunto de resultados generado por la cláusula FROM en particiones al que se aplica la función. Si no se especifica, la función trata todas las filas del conjunto de resultados de la consulta como un único grupo. *order_by_clause* determina el orden lógico en el que se realiza la operación. *order_by_clause* es necesario. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
 **float**  
  
## <a name="remarks"></a>Comentarios  
 Si se utiliza VAR en todos los elementos de una instrucción SELECT, cada valor del conjunto de resultados se incluye en el cálculo. VAR solo se puede utilizar con columnas numéricas. Se omiten los valores NULL.  
  
 VAR es una función determinista cuando se utiliza sin las cláusulas OVER y ORDER BY. Es no determinista si se especifica con las cláusulas OVER y ORDER BY. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-var"></a>R: utilizando VAR  
 El siguiente ejemplo devuelve la varianza para todos los valores de bonificación de la tabla `SalesPerson` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT VAR(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-var"></a>B: utilizando VAR  
 En el ejemplo siguiente se devuelve la varianza estadística de los valores de cuota de ventas en la tabla `dbo.FactSalesQuota`. La primera columna contiene la varianza de todos los valores distintos y la segunda columna contiene la varianza de todos los valores, incluidos los valores duplicados.  
  
```  
-- Uses AdventureWorks  
  
SELECT VAR(DISTINCT SalesAmountQuota)AS Distinct_Values, VAR(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
159180469909.18   158762853821.10
 ```  
  
### <a name="c-using-var-with-over"></a>C. Usar VAR con OVER  
 En el ejemplo siguiente se devuelve la varianza estadística de los valores de cuota de ventas para cada trimestre de un año natural. Observe que la cláusula ORDER BY en la cláusula OVER ordena la varianza estadística y la cláusula ORDER BY de la instrucción SELECT ordena el conjunto de resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       VAR(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Variance  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              Variance
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             1200500000.00
2002  3         70000.0000             1290333333.33
2002  4        154000.0000             1580250000.00
 ```  
  
## <a name="see-also"></a>Vea también  
 [Las funciones de agregado &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [EN cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  


