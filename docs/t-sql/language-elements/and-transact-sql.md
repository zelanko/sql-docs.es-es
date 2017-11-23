---
title: Y (Transact-SQL) | Documentos de Microsoft
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
- AND_TSQL
- AND
dev_langs: TSQL
helpviewer_keywords:
- values [SQL Server], TRUE
- TRUE
- AND, about AND operators
- AND
- combining expressions
ms.assetid: b61d7f8d-5a51-49b7-91dd-f6190a5a0fb9
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 34014541d124b0226218012d907fd2f99e0b1610
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="and-transact-sql"></a>AND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Combina dos expresiones booleanas y devuelve **TRUE** cuando ambas expresiones son **TRUE**. Cuando se utiliza más de un operador lógico en una instrucción, el **AND** operadores se evalúan primero. Puede cambiar el orden de evaluación gracias a los paréntesis.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
boolean_expression AND boolean_expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *boolean_expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que devuelve un valor booleano: **TRUE**, **FALSE**, o **desconocido**.  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="result-value"></a>Valor de resultado  
 Devuelve TRUE cuando ambas expresiones son TRUE.  
  
## <a name="remarks"></a>Comentarios  
 En la siguiente tabla se muestran los resultados de la comparación de los valores TRUE y FALSE mediante el operador AND.  
  
||TRUE|FALSE|UNKNOWN|  
|------|----------|-----------|-------------|  
|**ES TRUE**|TRUE|FALSE|UNKNOWN|  
|**FALSE**|FALSE|FALSE|FALSE|  
|**DESCONOCIDO**|UNKNOWN|FALSE|UNKNOWN|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-and-operator"></a>A. Utilizar el operador AND  
 En el ejemplo siguiente se selecciona información sobre los empleados que tienen el cargo de `Marketing Assistant` y más de `41` horas de vacaciones disponibles.  
  
```  
-- Uses AdventureWorks  
  
SELECT  BusinessEntityID, LoginID, JobTitle, VacationHours   
FROM HumanResources.Employee  
WHERE JobTitle = 'Marketing Assistant'  
AND VacationHours > 41 ;  
```  
  
### <a name="b-using-the-and-operator-in-an-if-statement"></a>B. Utilizar el operador AND en una instrucción IF  
 En los ejemplos siguientes se muestra cómo utilizar AND en una instrucción IF. En la primera instrucción, `1 = 1` y `2 = 2` son true; por consiguiente, el resultado es true. En el segundo ejemplo, el argumento `2 = 17` es false; por consiguiente, el resultado es false.  
  
```  
IF 1 = 1 AND 2 = 2  
BEGIN  
   PRINT 'First Example is TRUE'  
END  
ELSE PRINT 'First Example is FALSE';  
GO  
  
IF 1 = 1 AND 2 = 17  
BEGIN  
   PRINT 'Second Example is TRUE'  
END  
ELSE PRINT 'Second Example is FALSE' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [DONDE &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  
