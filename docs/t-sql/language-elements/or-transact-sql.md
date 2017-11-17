---
title: O (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
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
- OR_TSQL
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], combining
- combining conditions
- OR operator
ms.assetid: b730a256-4a63-4880-9906-65b05cd9caf2
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 590410dd84275f63bc610ac436410c7d323eb8e3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="or-transact-sql"></a>OR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Combina dos condiciones. Cuando en una instrucción se utiliza más de un operador lógico, los operadores OR se evalúan después de los operadores AND. Sin embargo, se puede cambiar el orden de evaluación gracias a los paréntesis.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
boolean_expression OR boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que devuelve TRUE, FALSE o UNKNOWN.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor de resultado  
 OR devuelve TRUE cuando alguna de las condiciones es TRUE.  
  
## <a name="remarks"></a>Comentarios  
 En la siguiente tabla se muestra el resultado del operador OR.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**ES TRUE**|TRUE|TRUE|TRUE|  
|**FALSE**|TRUE|FALSE|UNKNOWN|  
|**DESCONOCIDO**|TRUE|UNKNOWN|UNKNOWN|  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se utiliza la vista `vEmployeeDepartmentHistory` para recuperar los nombres del personal de `Quality Assurance` que trabaja en el turno de tarde o en el de noche. Si se omiten los paréntesis, la consulta devuelve los empleados de `Quality Assurance` que trabajan en el turno de tarde y todos los empleados que trabajan en el turno de noche.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Shift   
FROM HumanResources.vEmployeeDepartmentHistory  
WHERE Department = 'Quality Assurance'  
   AND (Shift = 'Evening' OR Shift = 'Night');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 FirstName    LastName         Shift 
 ------------ ---------------- ------- 
 Andreas      Berglund         Evening 
 Sootha       Charncherngkha   Night
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se recuperan los nombres de los empleados que cualquiera disfrutar de un `BaseRate` menos de 20 o tiene un `HireDate` el 1 de enero de 2001 o posterior.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, BaseRate, HireDate   
FROM DimEmployee  
WHERE BaseRate < 10 OR HireDate >= '2001-01-01';  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  



