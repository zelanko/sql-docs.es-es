---
title: 'SQL a C: Carácter ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3486c0fcf5cefc39c4b85af814d7d3c1d609b4e3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296675"
---
# <a name="sql-to-c-character"></a>SQL a C: Carácter

Los identificadores de los tipos de datos SQL ODBC de caracteres son los siguientes:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir datos SQL de caracteres. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  

|Identificador de tipo C|Prueba|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Longitud de bytes de los datos < *BufferLength*<br /><br /> Longitud de bytes de los datos >- *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes|N/D<br /><br /> 01004|  
|SQL_C_WCHAR|Longitud de caracteres de los datos < *BufferLength*<br /><br /> La longitud de los caracteres de los datos >- *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en caracteres<br /><br /> Longitud de los datos en caracteres|N/D<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Datos convertidos sin truncamiento[b]<br /><br /> Datos convertidos con truncamiento de dígitos fraccionarios[a]<br /><br /> La conversión de datos daría lugar a la pérdida de dígitos enteros (a diferencia de los fraccionarios)[a]<br /><br /> Los datos no son un *literal numérico*[b]|data<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|Número de bytes del tipo de datos C<br /><br /> Número de bytes del tipo de datos C<br /><br /> No definido<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Los datos están dentro del rango del tipo de datos al que se está convirtiendo el número[a]<br /><br /> Los datos están fuera del intervalo del tipo de datos al que se está convirtiendo el número[a]<br /><br /> Los datos no son un *literal numérico*[b]|data<br /><br /> No definido<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> No definido<br /><br /> No definido|N/D<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|Los datos son 0 o 1<br /><br /> Los datos son mayores que 0, menos que 2, y no iguales a 1<br /><br /> Los datos son menores o mayores o iguales que 2<br /><br /> Los datos no son un *literal numérico*|data<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|1[b]<br /><br /> 1[b]<br /><br /> No definido<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos|N/D<br /><br /> 01004|  
|SQL_C_TYPE_DATE|El valor de datos es un *valor de fecha*válido [a]<br /><br /> El valor de datos es un *valor de marca de tiempo*válido; porción de tiempo es cero[a]<br /><br /> El valor de datos es un *valor de marca de tiempo*válido; porción de tiempo es distinto de cero[a],[c]<br /><br /> El valor de datos no es un *valor de fecha-fecha* o *timestamp-valor*válido [a]|data<br /><br /> data<br /><br /> Datos truncados<br /><br /> No definido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> No definido|N/D<br /><br /> N/D<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|El valor de datos es un valor de tiempo válido y el valor de *fracciones de segundo es 0*[a]<br /><br /> El valor de datos es un valor de marca de tiempo válido *o un valor de tiempo válido;* fracción de segundos es cero[a],[d]<br /><br /> El valor de datos es un *valor de marca de tiempo*válido; fracción de segundos es distinto de cero[a],[d],[e]<br /><br /> El valor de datos no es un *valor de tiempo* válido o un valor de marca de *tiempo*[a]|data<br /><br /> data<br /><br /> Datos truncados<br /><br /> No definido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> No definido|N/D<br /><br /> N/D<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|El valor de datos es un valor de marca de tiempo válido *o un valor de tiempo válido;* porción de fracciones de segundo no truncada[a]<br /><br /> El valor de datos es un valor de marca de tiempo válido *o un valor de tiempo válido;* porción de fracciones de segundo truncada[a]<br /><br /> El valor de datos es un *valor de fecha*válido [a]<br /><br /> El valor de datos es un *valor de tiempo*válido [a]<br /><br /> El valor de datos no es un *valor de fecha-valor*válido, *valor de tiempo*o valor de marca de *tiempo*[a]|data<br /><br /> Datos truncados<br /><br /> Datos[f]<br /><br /> Datos[g]<br /><br /> No definido|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> N/D<br /><br /> N/D<br /><br /> 22018|  
|Todos los tipos de intervalo sC|El valor de datos es un valor de *intervalo*válido; sin truncamiento<br /><br /> El valor de datos es un valor de *intervalo*válido; truncamiento de uno o más campos finales<br /><br /> Los datos son un intervalo válido; campo líder se pierde una precisión significativa<br /><br /> El valor de datos no es un valor de intervalo válido|data<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] El valor de *BufferLength* se omite para esta conversión. El controlador supone que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] Este es el tamaño del tipo de datos C correspondiente.  
  
 [c] La parte de tiempo del *valor de marca* de tiempo se trunca.  
  
 [d] Se omite la parte de fecha del valor de marca de *tiempo.*  
  
 [e] La parte de fracciones de segundo de la marca de tiempo se trunca.  
  
 [f] Los campos de tiempo de la estructura de marca de tiempo se establecen en cero.  
  
 [g] Los campos de fecha de la estructura de marca de tiempo se establecen en la fecha actual.  

**Espacios adicionales**

Los espacios iniciales y finales se omiten cuando los datos de caracteres SQL se convierten en cualquiera de los siguientes tipos:

- date
- NUMERIC
- time
- timestamp
- datos del intervalo C
