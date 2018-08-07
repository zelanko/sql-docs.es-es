---
title: ABS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 46b2bf397563b61fad84c229496247245667bda4
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454269"
---
# <a name="abs-transact-sql"></a>ABS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Función matemática que devuelve el valor absoluto positivo de una expresión numérica específica. (`ABS` cambia los valores negativos por valores positivos. `ABS` no tiene ningún efecto en los valores cero o positivos).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ABS ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*numeric_expression*  
Una expresión de la categoría de tipo de datos numérico exacto o numérico aproximado.
  
## <a name="return-types"></a>Tipos devueltos  
Devuelve el mismo tipo que *numeric_expression*.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se muestra el resultado de usar la función `ABS` en tres números distintos.
  
```sql
SELECT ABS(-1.0), ABS(0.0), ABS(1.0);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---- ---- ----  
1.0  .0   1.0  
```  
  
La función `ABS` puede causar un error de desbordamiento cuando el valor absoluto de un número supera el número más grande que puede representar el tipo de datos especificado. Por ejemplo, el tipo de datos `int` tiene un rango de valores comprendido entre `-2,147,483,648` y `2,147,483,647`. El cálculo del valor absoluto del entero con signo `-2,147,483,648` causará un error de desbordamiento porque su valor absoluto supera el límite del intervalo positivo para el tipo de datos `int`.
  
```sql
DECLARE @i int;  
SET @i = -2147483648;  
SELECT ABS(@i);  
GO  
```  
  
Devuelve este mensaje de error:
  
"Mensaje 8115, nivel 16, estado 2, línea 3"
  
“Error de desbordamiento aritmético al convertir expresión al tipo de datos int”.

  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funciones integradas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)
  
  

