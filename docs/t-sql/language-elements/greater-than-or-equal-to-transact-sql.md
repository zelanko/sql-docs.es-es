---
title: '&gt;= (Mayor o igual que) (Transact-SQL) | Documentos de Microsoft'
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
- Greater
- '>='
- '>= (Greater Than or Equal To)'
- Equal To
- '>=_TSQL'
- Greater Than
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- greater than or equal to operator (>=)
- '>= (greater than or equal to operator)'
ms.assetid: 641ee28d-7536-46dd-a48a-6c63c2d59278
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3d062fde7d244e2b5697d68701315faa31671f57
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="gt-greater-than-or-equal-to-transact-sql"></a>&gt;= (Mayor o igual que) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Compara dos expresiones para "mayor o igual que" (un operador de comparación).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression >= expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md). Ambas expresiones deben tener tipos de datos que se puedan convertir implícitamente. La conversión depende de las reglas de [prioridad de tipo de datos](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 Boolean  
  
## <a name="remarks"></a>Comentarios  
 Cuando se comparan expresiones no nulas, el resultado es TRUE si el operando de la izquierda tiene un valor mayor que o igual al del operando de la derecha; de otra forma, el resultado es FALSE.  
  
 A diferencia del operador de igualdad =, el resultado de la comparación >= de dos valores NULL no depende del valor de ANSI_NULLS.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using--in-a-simple-query"></a>A. Usar >= en una consulta simple  
 En el ejemplo siguiente se devuelven todas las filas de la tabla `HumanResources.Department` que tienen un valor en `DepartmentID` que es mayor o igual que el valor 13.  
  
```  
-- Uses AdventureWorks  
  
SELECT DepartmentID, Name  
FROM HumanResources.Department  
WHERE DepartmentID >= 13  
ORDER BY DepartmentID;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
DepartmentID Name  
------------ --------------------------------------------------  
13           Quality Assurance  
14           Facilities and Maintenance  
15           Shipping and Receiving  
16           Executive  
  
(4 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [= &#40; Es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/equals-transact-sql.md)   
 [&#62; &#40; Mayor &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/greater-than-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
