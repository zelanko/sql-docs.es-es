---
title: "(División) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /
- /_TSQL
dev_langs: TSQL
helpviewer_keywords:
- / (divide)
- division [SQL Server]
- divide operator (/)
ms.assetid: 1d69893b-e5c3-441d-8dd8-0e5eb872ecfc
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a352cb9e3996a1199fd4a4c05f7ece7972cce1ee
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="-division-transact-sql"></a>/ (División) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Divide un número entre otro (es un operador aritmético de división).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
dividend / divisor  
```  
  
## <a name="arguments"></a>Argumentos  
 *dividend*  
 Es la expresión numérica que se va a dividir. *Dividendo* puede ser cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquiera de los tipos de datos de los valores numéricos de categoría, tipo de datos excepto la **datetime** y **smalldatetime** tipos de datos.  
  
 *divisor*  
 Es la expresión numérica entre la que se va a dividir el dividendo. *divisor* puede ser cualquier expresión válida de cualquiera de los tipos de datos de la categoría de tipo de datos numéricos, excepto el **datetime** y **smalldatetime** tipos de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
 Si es un entero *dividendo* se divide por un número entero *divisor*, el resultado es un entero que tiene cualquier parte fraccionaria del resultado truncado.  
  
## <a name="remarks"></a>Comentarios  
 El valor real que devuelve el operador / es el cociente de la primera expresión, dividida entre la segunda expresión.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se utiliza el operador aritmético de división para calcular el objetivo de ventas mensual para los vendedores en [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)].  
  
```  
-- Uses AdventureWorks  
  
SELECT s.BusinessEntityID AS SalesPersonID, FirstName, LastName, SalesQuota, SalesQuota/12 AS 'Sales Target Per Month'  
FROM Sales.SalesPerson AS s   
JOIN HumanResources.Employee AS e   
    ON s.BusinessEntityID = e.BusinessEntityID  
JOIN Person.Person AS p   
    ON e.BusinessEntityID = p.BusinessEntityID;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
```  
  
SalesPersonID FirstName    LastName          SalesQuota  Sales Target Per Month  
------------- ------------ ----------------- ----------- ------------------  
274           Stephen      Jiang             NULL        NULL  
275           Michael      Blythe            300000.00   25000.00  
276           Linda        Mitchell          250000.00   20833.3333  
277           Jillian      Carson            250000.00   20833.3333  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se usa el operador aritmético de división para calcular una proporción simple de horas de vacaciones de cada empleados en horas de baja por enfermedad.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, VacationHours/SickLeaveHours AS PersonalTimeRatio  
FROM DimEmployee;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)   
 [/ = &#40; asignación y división &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


