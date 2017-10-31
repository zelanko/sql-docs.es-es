---
title: TRIM (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: 4
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64cef84a613d71e65b33bed1c1e740dc59eeed9d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

Quita el carácter de espacio `char(32)` u otros caracteres especificados desde el principio o final de una cadena.  
 
## <a name="syntax"></a>Sintaxis   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[AMBOS | A LA IZQUIERDA | FINALES] no todavía disponibles."

## <a name="arguments"></a>Argumentos   

caracteres   
Es un literal, una variable o una llamada de función de cualquier tipo de carácter no LOB (`nvarchar`, `varchar`, `nchar`, o `char`) que contiene caracteres que se deben quitar. `nvarchar(max)`y `varchar(max)` no se permiten tipos.

string   
Es una expresión de cualquier tipo de caracteres (`nvarchar`, `varchar`, `nchar`, o `char`) donde se deben quitar los caracteres.

## <a name="return-types"></a>Tipos devueltos   
Devuelve una expresión de caracteres con un tipo de argumento de cadena donde el carácter de espacio `char(32)` o se quitan otros caracteres especificados de ambos lados. Devuelve `NULL` si la cadena de entrada es `NULL`.

## <a name="remarks"></a>Comentarios   
De forma predeterminada `TRIM` función quita el carácter de espacio `char(32)` de ambos lados. Es equivalente a `LTRIM(RTRIM(@string))`. Comportamiento de `TRIM ` función con los caracteres especificados es idéntico al comportamiento de `REPLACE` función donde se reemplazan los caracteres de inicio o finalización con cadenas vacías.


## <a name="examples"></a>Ejemplos
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Quita el carácter de espacio de ambos lados de cadena   
En el ejemplo siguiente se quita los espacios de antes y después de la palabra `test`.   
```tsql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  Quita los caracteres de ambos lados de cadena especificados   
En el ejemplo siguiente se quita un punto final y los espacios finales.
```tsql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>Vea también
[Funciones de cadena (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[LTRIM (Transact-SQL)](../../t-sql/functions/ltrim-transact-sql.md)   
[RTRIM (Transact-SQL)](../../t-sql/functions/rtrim-transact-sql.md)   
[REPLACE (Transact-SQL)](../../t-sql/functions/replace-transact-sql.md)   

