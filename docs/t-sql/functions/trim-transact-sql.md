---
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a7854b2419b3644c2f3c76cd96cccc06bfae2902
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2019
ms.locfileid: "54299622"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Comparta sus comentarios sobre la tabla de contenido de la documentación de SQL.](https://aka.ms/sqldocsurvey)

Quita el carácter de espacio `char(32)` (u otros caracteres especificados) del principio o del final de una cadena.  
 
## <a name="syntax"></a>Sintaxis   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[ BOTH | LEADING | TRAILING ] aún no disponibles."

## <a name="arguments"></a>Argumentos   

caracteres   
Es un literal, una variable o una llamada de función de cualquier tipo de carácter no de LOB (`nvarchar`, `varchar`, `nchar` o `char`) que contiene caracteres que se deben quitar. Los tipos `nvarchar(max)` y `varchar(max)` no se permiten.

string   
Es una expresión de cualquier tipo de carácter (`nvarchar`, `varchar`, `nchar` o `char`) donde se deben quitar caracteres.

## <a name="return-types"></a>Tipos devueltos   
Devuelve una expresión de caracteres con un tipo de argumento de cadena donde el carácter de espacio `char(32)` u otros caracteres especificados se quitan de ambos lados. Devuelve `NULL` si la cadena de entrada es `NULL`.

## <a name="remarks"></a>Notas   
La función `TRIM` quita el carácter de espacio `char(32)` de ambos lados de forma predeterminada. Es equivalente a `LTRIM(RTRIM(@string))`. El comportamiento de la función `TRIM ` con los caracteres especificados es idéntico al comportamiento de la función `REPLACE`, donde los caracteres de inicio o finalización se reemplazan por cadenas vacías.


## <a name="examples"></a>Ejemplos
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Quitar el carácter de espacio de ambos lados de la cadena   
En el siguiente ejemplo se quitan los espacios que van antes y después de la palabra `test`.   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>b.  Quitar los caracteres especificados de ambos lados de la cadena   
En el siguiente ejemplo se quita un punto final y los espacios finales.
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>Consulte también
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
