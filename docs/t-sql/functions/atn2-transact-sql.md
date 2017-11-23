---
title: ATN2 (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ATN2
- ATN2_TSQL
dev_langs: TSQL
helpviewer_keywords:
- arctangent
- tangent
- ATN2 function
ms.assetid: 014b291e-7cd7-4c39-b20d-5db3a9f0505d
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 022c5cd7655debb529ec00789f075d95278073f6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="atn2-transact-sql"></a>ATN2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
[float y real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
[Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  

