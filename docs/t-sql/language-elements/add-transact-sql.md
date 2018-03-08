---
title: + (Suma) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
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
- add
- +
- +_TSQL
- + (Add)
dev_langs:
- TSQL
helpviewer_keywords:
- addition (+)
- adding numbers
- + (add)
- plus sign (+)
- add operator (+)
ms.assetid: 4ba8baac-5f07-432c-87c5-d23e7011da55
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0c9aca952ab6853a2456b95dab912092d7708668
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="-addition-transact-sql"></a>+ (Suma) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Suma dos números. Este operador aritmético de suma también puede sumar un número, en días, a una fecha.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression + expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de uno de los datos de tipos de la categoría numérica, excepto el **bits** tipo de datos. No se puede usar con **fecha**, **tiempo**, **datetime2**, o **datetimeoffset** tipos de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-addition-operator-to-calculate-the-total-number-of-hours-away-from-work-for-each-employee"></a>A. Utilizar el operador de suma para calcular el número total de horas que cada empleado ha dejado de trabajar  
 Este ejemplo busca el número total de horas de trabajo para cada empleado sumando el número de horas utilizadas como vacaciones y el número de horas utilizadas como baja por enfermedad.  
  
```  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, VacationHours, SickLeaveHours,   
    VacationHours + SickLeaveHours AS 'Total Hours Away'  
FROM HumanResources.Employee AS e  
    JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
ORDER BY 'Total Hours Away' ASC;  
GO  
```  
  
### <a name="b-using-the-addition-operator-to-add-days-to-date-and-time-values"></a>B. Utilizar el operador de suma para sumar días a valores de fecha y hora  
 Este ejemplo agrega un número de días que un `datetime` fecha.  
  
```  
  
SET NOCOUNT ON  
DECLARE @startdate datetime, @adddays int;  
SET @startdate = ''January 10, 1900 12:00 AM';  
SET @adddays = 5;  
SET NOCOUNT OFF;  
SELECT @startdate + 1.25 AS 'Start Date',   
   @startdate + @adddays AS 'Add Date';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Start Date                  Add Date
--------------------------- ---------------------------
1900-01-11 06:00:00.000     1900-01-15 00:00:00.000
  
(1 row(s) affected)
 ```  
  
### <a name="c-adding-character-and-integer-data-types"></a>C. Sumar tipos de datos character e integer  
 En el ejemplo siguiente se agrega un **int** valor y un valor de carácter de tipo de datos al convertir el tipo de datos de carácter **int**. Si existe un carácter que no es válido en el **char** cadena, la [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve un error.  
  
```  
DECLARE @addvalue int;  
SET @addvalue = 15;  
SELECT '125127' + @addvalue;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-----------------------
125142
  
(1 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-the-addition-operator-to-calculate-the-total-number-of-hours-away-from-work-for-each-employee"></a>Utilizar el operador de suma para calcular el número total de horas de trabajo para cada empleado D:  
 En el ejemplo siguiente se busca el número total de horas de trabajo para cada empleado sumando el número de horas utilizadas como vacaciones y el número de horas utilizadas como baja por enfermedad y ordena los resultados en orden ascendente.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, VacationHours, SickLeaveHours,   
    VacationHours + SickLeaveHours AS TotalHoursAway  
FROM DimEmployee  
ORDER BY TotalHoursAway ASC;  
```  
  
## <a name="see-also"></a>Vea también  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [+= &#40;Addition Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)   
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  


