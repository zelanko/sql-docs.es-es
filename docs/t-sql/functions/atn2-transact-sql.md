---
title: ATN2 (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ATN2
- ATN2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- arctangent
- tangent
- ATN2 function
ms.assetid: 014b291e-7cd7-4c39-b20d-5db3a9f0505d
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 3c68b65c2bde2d8b4c5cd8f34452563b433c6a29
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="atn2-transact-sql"></a>ATN2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el ángulo (en radianes) formado por el eje X positivo y la línea que se extiende desde el origen al punto (y, x), donde x e y son los valores de las dos expresiones de punto flotante especificadas.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ATN2 ( float_expression , float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression* es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de la **float** tipo de datos.
  
## <a name="return-types"></a>Tipos de valor devuelto
**float**
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se calcula el `ATN2` de los componentes `x` e `y` especificados.
  
```sql
DECLARE @x float = 35.175643, @y float = 129.44;  
SELECT 'The ATN2 of the angle is: ' + CONVERT(varchar,ATN2(@x,@y ));  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
The ATN2 of the angle is: 0.265345                         
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[float y real & #40; Transact-SQL & #41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
[Funciones matemáticas & #40; Transact-SQL & #41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


