---
title: STDEV (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDEV_TSQL
- STDEV
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], statistical standard deviation
- STDEV function [Transact-SQL]
- statistical standard deviation
ms.assetid: ff41b4fc-4f71-4f18-bf78-96614ea908cc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 687eced9434fa57f2cc7a8449de9e2346afeb16c
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947638"
---
# <a name="stdev-transact-sql"></a>STDEV (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la desviación típica estadística de todos los valores de la expresión especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```    
-- Aggregate Function Syntax   
STDEV ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax   
STDEV ([ ALL ] expression) OVER ( [ partition_by_clause ] order_by_clause)  
```  
  
## <a name="arguments"></a>Argumentos  
 **ALL**  
 Aplica la función a todos los valores. ALL es el valor predeterminado.  
  
 DISTINCT  
 Especifica que se tiene en cuenta cada valor único.  
  
 *expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) numérica. No se permiten funciones de agregado ni subconsultas. *expression* es una expresión de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos **bit**.  
  
 OVER **(** [ *partition_by_clause* ] _order\_by\_clause_ **)**  
 _partition\_by\_clause_ divide el conjunto de resultados generado por la cláusula FROM en particiones a las que se aplica la función. Si no se especifica, la función trata todas las filas del conjunto de resultados de la consulta como un único grupo. _order\_by\_clause_ determina el orden lógico en el que se realiza la operación. _order\_by\_clause_ es obligatorio. Para más información, vea [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
 **float**  
  
## <a name="remarks"></a>Notas  
 Si STDEV se utiliza en todos los elementos de una instrucción SELECT, en el cálculo se incluirán todos los valores del conjunto de resultados. STDEV solo puede utilizarse con columnas numéricas. Se omiten los valores NULL.  
  
 STDEV es una función determinista cuando se utiliza sin las cláusulas OVER y ORDER BY. Es no determinista si se especifica con las cláusulas OVER y ORDER BY. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-stdev"></a>A. Con STDEV  
 En el ejemplo siguiente se devuelve la desviación estándar de todos los valores de bonificación de la tabla `SalesPerson` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT STDEV(Bonus)  
FROM Sales.SalesPerson;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-using-stdev"></a>B. Con STDEV  
 En el siguiente ejemplo se obtiene la desviación típica de los valores de cuota de ventas en la tabla `dbo.FactSalesQuota`. La primera columna contiene la desviación estándar de todos los valores distintos y la segunda columna contiene la desviación estándar de todos los valores, incluidos los valores duplicados.  
  
```  
-- Uses AdventureWorks  
  
SELECT STDEV(DISTINCT SalesAmountQuota)AS Distinct_Values, STDEV(SalesAmountQuota) AS All_Values  
FROM dbo.FactSalesQuota;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Distinct_Values   All_Values
----------------  ----------------
398974.27         398450.57
 ```  
  
### <a name="c-using-stdev-with-over"></a>C. Con STDEVP y OVER  
 En este ejemplo se devuelve la desviación típica de los valores de cuota de ventas de cada trimestre de un año natural. Observe que ORDER BY en la cláusula OVER ordena STDEV, mientras que ORDER BY de la instrucción SELECT ordena el conjunto de resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       STDEV(SalesAmountQuota) OVER (ORDER BY CalendarYear, CalendarQuarter) AS StdDeviation  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear = 2002  
ORDER BY CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Year  Quarter  SalesQuota              StdDeviation
----  -------  ----------------------  -------------------
2002  1         91000.0000             null
2002  2        140000.0000             34648.23
2002  3         70000.0000             35921.21
2002  4        154000.0000             39752.36
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de agregado &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [OVER &#40;cláusula de Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)  
  
  

