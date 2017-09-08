---
title: "Funciones matemáticas (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- calculations [SQL Server]
- mathematical functions [SQL Server]
- functions [SQL Server], mathematical
ms.assetid: 46495a2e-81d0-4677-9d72-9db083cd1023
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5ec4a6767acab606d6459b439683a88a0cae1caf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mathematical-functions-transact-sql"></a>Funciones matemáticas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Las siguientes funciones escalares realizan un cálculo, normalmente basado en valores de entrada proporcionados como argumentos, y devuelven un valor numérico:  
  
||||  
|-|-|-|  
|[ABS](../../t-sql/functions/abs-transact-sql.md)|[GRADOS](../../t-sql/functions/degrees-transact-sql.md)|[RAND](../../t-sql/functions/rand-transact-sql.md)|  
|[ACOS](../../t-sql/functions/acos-transact-sql.md)|[EXP](../../t-sql/functions/exp-transact-sql.md)|[REDONDEAR](../../t-sql/functions/round-transact-sql.md)|  
|[ASIN](../../t-sql/functions/asin-transact-sql.md)|[FLOOR](../../t-sql/functions/floor-transact-sql.md)|[INICIO DE SESIÓN](../../t-sql/functions/sign-transact-sql.md)|  
|[ATAN](../../t-sql/functions/atan-transact-sql.md)|[REGISTRO](../../t-sql/functions/log-transact-sql.md)|[SENO](../../t-sql/functions/sin-transact-sql.md)|  
|[ATN2](../../t-sql/functions/atn2-transact-sql.md)|[LOG10](../../t-sql/functions/log10-transact-sql.md)|[SQRT](../../t-sql/functions/sqrt-transact-sql.md)|  
|[LÍMITE SUPERIOR](../../t-sql/functions/ceiling-transact-sql.md)|[PI](../../t-sql/functions/pi-transact-sql.md)|[CUADRADO](../../t-sql/functions/square-transact-sql.md)|  
|[COS](../../t-sql/functions/cos-transact-sql.md)|[POWER](../../t-sql/functions/power-transact-sql.md)|[TAN](../../t-sql/functions/tan-transact-sql.md)|  
|[COT](../../t-sql/functions/cot-transact-sql.md)|[RADIANES](../../t-sql/functions/radians-transact-sql.md)||  
  
> [!NOTE]  
>  Las funciones aritméticas, como ABS, CEILING, DEGREES, FLOOR, POWER, RADIANS y SIGN, devuelven un valor del mismo tipo de datos que el valor de entrada. Funciones trigonométricas y otras funciones, incluidas EXP, LOG, LOG10, SQUARE y SQRT, conversión los valores de entrada a **float** y devolver un **float** valor.  
  
 Todas las funciones matemáticas, excepto RAND, son deterministas, lo que significa que devuelven el mismo resultado cada vez que se llaman con un conjunto específico de valores de entrada. RAND es determinista solo cuando se especifica un parámetro de inicialización. Para obtener más información acerca del determinismo de función, vea [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="see-also"></a>Vea también  
  [Operadores aritméticos &#40; Transact-SQL &#41;](../../t-sql/language-elements/arithmetic-operators-transact-sql.md)  
  [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  

