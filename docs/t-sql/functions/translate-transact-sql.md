---
title: TRADUCIR (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords: TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: "5"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e7ea679043b83d8cee26f431602450d023516647
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="translate-transact-sql"></a>TRADUCIR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve la cadena proporcionada como primer argumento después de algunos caracteres especificados en el segundo argumento se convierten en un conjunto de destinos de caracteres.

## <a name="syntax"></a>Sintaxis   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>Argumentos   

inputString   
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de caracteres (nvarchar, varchar, nchar, char).

caracteres   
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo de caracteres que contiene caracteres que se deben reemplazar.

traducciones   
Es un carácter [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que coincida con el segundo argumento según el tipo y longitud.

## <a name="return-types"></a>Tipos devueltos   
Devuelve una expresión de caracteres del mismo tipo como `inputString` donde se reemplazan los caracteres del segundo argumento con los caracteres coincidentes del tercer argumento.

## <a name="remarks"></a>Comentarios   

`TRANSLATE`función devolverá un error si los caracteres y traducciones tienen longitudes diferentes. `TRANSLATE`función debe devolver la entrada sin cambios si los valores null se proporcionan como argumentos de reemplazo o caracteres. El comportamiento de la `TRANSLATE` función debería ser idéntica a la [reemplazar](../../t-sql/functions/replace-transact-sql.md) función.   

El comportamiento de la `TRANSLATE` función es equivalente a utilizar varios `REPLACE` funciones.

`TRANSLATE`es siempre intercalación de SC consciente.

## <a name="examples"></a>Ejemplos   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. Reemplace llaves cuadrados y llaves con llaves regulares    
La siguiente consulta reemplaza cuadrados y las llaves en la cadena de entrada entre paréntesis:
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  El `TRANSLATE` función en este ejemplo es equivalente a pero mucho más sencilla que la siguiente instrucción mediante `REPLACE`:`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. Convertir los puntos GeoJSON WKT    
GeoJSON es un formato para la codificación de una variedad de estructuras de datos geográficos. Con el `TRANSLATE` función, los desarrolladores pueden convertir fácilmente los puntos GeoJSON a formato WKT y viceversa. La siguiente consulta reemplaza cuadrados y las llaves de entrada con llaves regulares:   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|Punto  |Coordenadas |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>Vea también
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [Funciones de cadena (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   

