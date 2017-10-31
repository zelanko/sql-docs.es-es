---
title: "Precisión, escala y longitud (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 7/22/2017
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
- data types [SQL Server], length
- data types [SQL Server], scale
- precision [SQL Server], data types
- lengths [SQL Server], data types
- number of digits
- scale [SQL Server]
- scale [SQL Server], data types
- data types [SQL Server], precision
ms.assetid: fbc9ad2c-0d3b-4e98-8fdd-4d912328e40a
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 557d7a5c45e9cc5a0839dfb4a1fdb0d08c2bf83f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="precision-scale-and-length-transact-sql"></a>Precisión, escala y longitud (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

La precisión es el número de dígitos de un número. La escala es el número de dígitos situados a la derecha de la coma decimal de un número. Por ejemplo, el número 123,45 tiene una precisión de 5 y una escala de 2.
  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la precisión máxima predeterminada de **numérico** y **decimal** tipos de datos es 38. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el valor máximo predeterminado es 28.
  
La longitud de un tipo de datos numérico es el número de bytes utilizados para almacenar el número. La longitud para una cadena de caracteres o tipo de datos Unicode es el número de caracteres. La longitud de **binario**, **varbinary**, y **imagen** tipos de datos es el número de bytes. Por ejemplo, un **int** tipo de datos puede contener 10 dígitos, se almacena en 4 bytes y no acepta coma decimal. El **int** tipo de datos tiene una precisión de 10, una longitud de 4 y una escala de 0.
  
Cuando dos **char**, **varchar**, **binario**, o **varbinary** se concatenan expresiones, la longitud de la expresión resultante es el suma de las longitudes de las dos expresiones de origen o 8.000 caracteres, lo que sea menor.
  
Cuando dos **nchar** o **nvarchar** se concatenan expresiones, la longitud de la expresión resultante es la suma de las longitudes de las dos expresiones de origen o 4.000 caracteres, lo que sea menor.
  
Cuando se comparan dos expresiones del mismo tipo de datos pero de distintas longitudes mediante UNION, EXCEPT o INTERSECT, la longitud resultante es la longitud máxima de las dos expresiones.
  
La precisión y escala de los tipos de datos numéricos además **decimal** son fijos. Si un operador aritmético tiene dos expresiones del mismo tipo, el resultado tiene el mismo tipo de datos con la precisión y la escala definidas para ese tipo de datos. Si un operador tiene dos expresiones con tipos de datos numéricos diferentes, las reglas de prioridad de tipos de datos definen el tipo de datos del resultado. El resultado tiene la precisión y la escala definidas para el tipo de datos que le corresponde.
  
La siguiente tabla define cómo se calculan la precisión y la escala del resultado cuando el resultado de una operación es de tipo **decimal**. El resultado es **decimal** cuando alguna de las acciones siguientes sea verdadera:
-   Ambas expresiones son **decimal**.  
-   Una expresión es **decimal** y el otro es un tipo de datos con una precedencia menor que **decimal**.  
  
Las expresiones de operando se denotan como expresión e1, con precisión p1 y escala s1, y expresión e2, con precisión p2 y escala s2. La precisión y escala de cualquier expresión que no es **decimal** es la precisión y la escala definidas para el tipo de datos de la expresión.
  
|Operación|Precisión del resultado|Escala del resultado *|  
|---|---|---|
|e1 + e2|máx(s1, s2) + máx(p1-s1, p2-s2) + 1|máx(s1, s2)|  
|e1 - e2|máx(s1, s2) + máx(p1-s1, p2-s2) + 1|máx(s1, s2)|  
|e1 * e2|p1 + p2 + 1|s1 + s2|  
|e1 / e2|p1 - s1 + s2 + máx(6, s1 + p2 + 1)|máx(6, s1 + p2 + 1)|  
|E1 {UNION &#124; EXCEPTO &#124; INTERSECT} e2|máx(s1, s2) + máx(p1-s1, p2-s2)|máx(s1, s2)|  
|e1 % e2|min(p1-s1, p2 -s2) + max( s1,s2 )|máx(s1, s2)|  
  
\*La precisión del resultado y la escala tiene un máximo absoluto igual a 38. Cuando una precisión del resultado es mayor que 38, se reduce a 38 y la escala correspondiente se reduce para impedir que la parte entera de un resultado que se va a truncar. En algunos casos, como la multiplicación o la división, factor de escala no se reducirá para mantener la precisión decimal, aunque se puede generar el error de desbordamiento.

En las operaciones de suma y resta necesitamos `max(p1 – s1, p2 – s2)` que se van a almacenar parte integral del número decimal. Si no hay suficiente espacio para almacenarlas es decir, `max(p1 – s1, p2 – s2) < min(38, precision) – scale`, se reduce la escala para proporcionar suficiente espacio para la parte entera. Escala resultante es `MIN(precision, 38) - max(p1 – s1, p2 – s2)`, por lo que la parte fraccionaria podría redondeará para ajustarse a la escala resultante.

En las operaciones de multiplicación y división necesitamos `precision - scale` que se van a almacenar la parte entera del resultado. La escala podría reducirse, utilizando las reglas siguientes:
1.  La escala resultante se reduce a `min(scale, 38 – (precision-scale))` si la parte entera es menor que 32, porque no puede ser mayor que `38 – (precision-scale)`. Resultado podría redondearse en este caso.
1. No se cambiará la escala si es inferior a 6 y la parte entera es mayor que 32. En este caso, podría producirá un error de desbordamiento si no cabe en decimal (38, escala) 
1. La escala se establecerá en 6 si es superior a 6 y la parte entera es mayor que 32. En este caso, se reducirían parte integral y escala y el tipo resultante es decimal(38,6). Resultado podría se redondea hasta 6 posiciones decimales o se producirá un error de desbordamiento si parte entera no cabe en 32 dígitos.

## <a name="examples"></a>Ejemplos
La siguiente expresión devuelve resultados `0.00000090000000000` sin redondeo, porque el resultado puede caber en `decimal(38,17)`:
```sql
select cast(0.0000009000 as decimal(30,20)) * cast(1.0000000000 as decimal(30,20)) [decimal 38,17]
```
En este caso, la precisión es 61 y escala es 40.
Parte integral (escala de precisión = 21) es menor que 32, por lo que se trata de caso (1) en las reglas de multiplicación y escala se calcula como `min(scale, 38 – (precision-scale)) = min(40, 38 – (61-40)) = 17`. Tipo de resultado es `decimal(38,17)`.

La siguiente expresión devuelve resultados `0.000001` para caber en `decimal(38,6)`:
```sql
select cast(0.0000009000 as decimal(30,10)) * cast(1.0000000000 as decimal(30,10)) [decimal(38, 6)]
```
En este caso, la precisión es 61 y escala es 20.
Escala es mayor que la parte entera y 6 (`precision-scale = 41`) es mayor que 32. Éste es el caso (3) en las reglas de multiplicación y tipo de resultado es `decimal(38,6)`.

## <a name="see-also"></a>Vea también
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

