---
title: ABS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ABS_TSQL
- ABS
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], positive
- values [SQL Server], absolute
- ABS function
- absolute positive value
ms.assetid: e2ea7a6d-3e2f-472c-afbc-437d3b835c03
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9f96d651f179120fab6fabfb78d08cca84404bd1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Función matemática que devuelve el valor absoluto positivo de una expresión numérica específica. (`ABS` cambios de los valores a valores positivos negativos. `ABS`no tiene ningún efecto en cero o valores positivos.)
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*numeric_expression*  
Es una expresión de la categoría de tipo de datos numérico exacto o numérico aproximado.
  
## <a name="return-types"></a>Tipos devueltos  
Devuelve el mismo tipo que *numeric_expression*.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se muestra el resultado de usar la función `ABS` en tres números distintos.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
La función `ABS` puede causar un error de desbordamiento cuando el valor absoluto de un número es mayor que el número más grande que puede representar el tipo de datos especificado. Por ejemplo, el tipo de datos `int` solo puede contener valores de `-2,147,483,648` a `2,147,483,647`. El cálculo del valor absoluto del entero con signo `-2,147,483,648` causa un error de desbordamiento porque su valor absoluto es mayor que el intervalo positivo para el tipo de datos `int`.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Éste es el mensaje de error:
  
"Mensaje 8115, nivel 16, estado 2, línea 3"
  
“Error de desbordamiento aritmético al convertir expresión al tipo de datos int”.

  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funciones integradas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

