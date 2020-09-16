---
description: TRIM (Transact-SQL)
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
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
author: julieMSFT
ms.author: jrasnick
monikerRange: = azure-sqldw-latest||=azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d37d26a54bb3659f7cd1fe929d8fbf1ee48624e
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076722"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

Esto permite quitar el carácter de espacio `char(32)` (u otros caracteres especificados) del principio y del final de una cadena.  

## <a name="syntax"></a>Sintaxis

```
-- Syntax for SQL Server and Azure SQL Database
TRIM ( [ characters FROM ] string )
```

```
-- Syntax for Azure Synapse Analytics
TRIM ( string )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos

"characters" es un literal, una variable o una llamada de función de cualquier tipo de carácter no de LOB (`nvarchar`, `varchar`, `nchar` o `char`) que contiene caracteres que se deben quitar. Los tipos `nvarchar(max)` y `varchar(max)` no se permiten.

"string" es una expresión de cualquier tipo de carácter (`nvarchar`, `varchar`, `nchar` o `char`) donde se deben quitar caracteres.

## <a name="return-types"></a>Tipos de valor devuelto

Devuelve una expresión de caracteres con un tipo de argumento de cadena donde el carácter de espacio `char(32)` u otros caracteres especificados se quitan de ambos lados. Devuelve `NULL` si la cadena de entrada es `NULL`.

## <a name="remarks"></a>Observaciones

De manera predeterminada, la función `TRIM` quita el carácter de espacio de los extremos de inicio y final de la cadena. Este comportamiento equivale a `LTRIM(RTRIM(@string))`.

## <a name="examples"></a>Ejemplos

### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  Quitar el carácter de espacio de ambos lados de la cadena

En el siguiente ejemplo se quitan los espacios que van antes y después de la palabra `test`.

```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```
test
```

### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  Quitar los caracteres especificados de ambos lados de la cadena

En el ejemplo siguiente se quitan los espacios y el punto final antes de `#` y después de la palabra `test`.

```sql
SELECT TRIM( '.,! ' FROM  '     #     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
#     test
```

## <a name="see-also"></a>Consulte también

- [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
- [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
- [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
- [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
- [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
- [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
- [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
