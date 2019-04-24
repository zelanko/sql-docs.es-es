---
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7734ce09ca33c1db8b0ab650509edeabe9e80a08
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2019
ms.locfileid: "59670861"
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Devuelve la cadena proporcionada como primer argumento después de que algunos caracteres especificados en el segundo argumento se hayan convertido en un conjunto de destino de caracteres especificado en el tercer argumento.

## <a name="syntax"></a>Sintaxis

```sql
TRANSLATE ( inputString, characters, translations)
```

## <a name="arguments"></a>Argumentos

 *inputString* es la [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cadena que se va a buscar. *inputString* puede ser cualquier tipo de datos de carácter (nvarchar, varchar, nchar, char).

 *characters* es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cadena que contiene caracteres que se deben reemplazar. *characters* puede ser cualquier tipo de datos de caracteres.

*translations* es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cadena que contiene los caracteres de reemplazo. *translations* debe tener el mismo tipo de datos y la misma longitud que *characters*.

## <a name="return-types"></a>Tipos devueltos

Devuelve una expresión de caracteres del mismo tipo de datos que `inputString`, donde se reemplazan los caracteres del segundo argumento con los caracteres coincidentes del tercer argumento.

## <a name="remarks"></a>Notas

La función `TRANSLATE` devolverá un error si las expresiones *characters* y *translations* tienen longitudes diferentes. `TRANSLATE` devolverá NULL si alguno de los argumentos es NULL.  

El comportamiento de la función `TRANSLATE` es equivalente a usar varias funciones [REPLACE](../../t-sql/functions/replace-transact-sql.md). Pero `TRANSLATE` no reemplaza un carácter más de una vez. Esto es diferente a varias funciones `REPLACE`, ya que en cada uso se reemplazarían todos los caracteres pertinentes. 

`TRANSLATE` siempre reconoce la intercalación de SC.

## <a name="examples"></a>Ejemplos

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. Reemplazar corchetes y llaves con llaves normales

En esta consulta se reemplazan corchetes y llaves en la cadena de entrada entre paréntesis:

```sql
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

```plain_text
2*(3+4)/(7-2)
```

#### <a name="equivalent-calls-to-replace"></a>Llamadas equivalentes a REPLACE

En la siguiente instrucción SELECT, hay un grupo de cuatro llamadas anidadas a la función REPLACE. Este grupo es equivalente a la llamada realizada a la función TRANSLATE de la instrucción SELECT anterior:

```sql
SELECT
REPLACE
(
      REPLACE
      (
            REPLACE
            (
                  REPLACE
                  (
                        '2*[3+4]/{7-2}',
                        '[',
                        '('
                  ),
                  ']',
                  ')'
            ),
            '{',
            '('
      ),
      '}',
      ')'
);
```

### <a name="b-convert-geojson-points-into-wkt"></a>B. Convertir puntos GeoJSON en WKT

GeoJSON es un formato para codificar una variedad de estructuras de datos geográficos. Con la función `TRANSLATE`, los desarrolladores pueden convertir fácilmente los puntos GeoJSON a formato WKT y viceversa. En esta consulta se reemplazan corchetes y llaves en la entrada con llaves normales:

```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]

|Punto  |Coordenadas |  
|---------|--------- |
|(137.4  72.3) |[137.4,72.3] |

### <a name="c-use-the-translate-function"></a>C. Uso de la función TRANSLATE

```sql
SELECT TRANSLATE('abcdef','abc','bcd') AS Translated,
       REPLACE(REPLACE(REPLACE('abcdef','a','b'),'b','c'),'c','d') AS Replaced;
```

Los resultados son:

| Traducidos | Reemplazados |  
| ---------|--------- |
| bcddef | ddddef |


## <a name="see-also"></a>Consulte también

 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [String Functions (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md) [Funciones de cadena (Transact-SQL)]
