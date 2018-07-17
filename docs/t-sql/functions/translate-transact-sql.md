---
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 6aa2621c9ff7a2ea9301384c9aab81df7f7144ad
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37784376"
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve la cadena proporcionada como primer argumento después de que algunos caracteres especificados en el segundo argumento se hayan convertido en un conjunto de destino de caracteres.

## <a name="syntax"></a>Sintaxis   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>Argumentos   

inputString   
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de carácter (nvarchar, varchar, nchar, char).

caracteres   
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de carácter que contenga caracteres que se deben reemplazar.

traducciones   
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de caracteres que coincide con el segundo argumento según el tipo y longitud.

## <a name="return-types"></a>Tipos devueltos   
Devuelve una expresión de caracteres del mismo tipo que `inputString`, donde se reemplazan los caracteres del segundo argumento con los caracteres coincidentes del tercer argumento.

## <a name="remarks"></a>Notas   

La función `TRANSLATE` devolverá un error si los caracteres y las traducciones tienen longitudes diferentes. La función `TRANSLATE` debe devolver la entrada sin cambios si los valores null se proporcionan como argumentos de reemplazo o caracteres. El comportamiento de la función `TRANSLATE` debe ser idéntico a la función [REPLACE](../../t-sql/functions/replace-transact-sql.md).   

El comportamiento de la función `TRANSLATE` es equivalente a usar varias funciones `REPLACE`.

`TRANSLATE` siempre reconoce la intercalación de SC.

## <a name="examples"></a>Ejemplos   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. Reemplazar corchetes y llaves con llaves normales    
En esta consulta se reemplazan corchetes y llaves en la cadena de entrada entre paréntesis:
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  La función `TRANSLATE` de este ejemplo equivale, aunque es mucho más sencilla, a la siguiente instrucción mediante `REPLACE`: `SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. Convertir puntos GeoJSON en WKT    
GeoJSON es un formato para codificar una variedad de estructuras de datos geográficos. Con la función `TRANSLATE`, los desarrolladores pueden convertir fácilmente los puntos GeoJSON a formato WKT y viceversa. En esta consulta se reemplazan corchetes y llaves en la entrada con llaves normales:   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|Punto  |Coordenadas |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>Ver también
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

