---
title: 'SQL a C: Carácter | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3a0a7036d67716a3d90bd8953a3c7ba2c575c92
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/22/2019
ms.locfileid: "54419980"
---
# <a name="sql-to-c-character"></a>SQL a C: Carácter

Los identificadores de los tipos de datos SQL de ODBC de caracteres son los siguientes:

- SQL_CHAR
- SQL_VARCHAR
- SQL_LONGVARCHAR
- SQL_WCHAR
- SQL_WVARCHAR
- SQL_WLONGVARCHAR

La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de SQL de caracteres de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo de C|Prueba|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|
|:----------------|:---|:-------------|:---------------|:-------|
|SQL_C_CHAR|Longitud de bytes de datos < *BufferLength*<br /><br /> Longitud de bytes de datos > = *BufferLength*|Datos<br /><br /> Datos truncados|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Longitud de datos de caracteres < *BufferLength*<br /><br /> Longitud de datos de caracteres > = *BufferLength*|Datos<br /><br /> Datos truncados|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT  SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT  SQL_C_SLONG SQL_C_ULONG SQL_C_LONG  SQL_C_NUMERIC|Convierten datos sin truncamiento [b]<br /><br /> Convierten datos con el truncamiento de dígitos fraccionarios [a]<br /><br /> Conversión de datos daría lugar a pérdida de dígitos de entero (en contraposición a fraccionarios) [a]<br /><br /> Datos no están un *literales numéricos*[b].|Datos<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|Número de bytes del tipo de datos C<br /><br /> Número de bytes del tipo de datos C<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Datos están dentro del intervalo del tipo de datos a la que se va a convertir el número de [a]<br /><br /> Datos están fuera del intervalo del tipo de datos a la que se va a convertir el número de [a]<br /><br /> Datos no están un *literales numéricos*[b].|Datos<br /><br /> No definido<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BIT|Datos están 0 o 1<br /><br /> Datos están mayores que 0, inferior a 2 y no es igual a 1<br /><br /> Datos están menor que 0 o mayor que o igual a 2<br /><br /> Datos no están un *literales numéricos*|Datos<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|1[b]<br /><br /> 1[b]<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|Datos<br /><br /> Datos truncados|Longitud de datos en bytes<br /><br /> Longitud de datos|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Valor de datos es válido *valor de fecha*[a]<br /><br /> Valor de datos es válido *valor de marca de tiempo*; parte de hora es cero [a]<br /><br /> Valor de datos es válido *valor de marca de tiempo*; parte de hora es distinto de cero [a], [c]<br /><br /> Valor de datos no es válido *valor de fecha* o *valor de marca de tiempo*[a]|Datos<br /><br /> Datos<br /><br /> Datos truncados<br /><br /> No definido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> No definido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Valor de datos es válido *valor de hora y las fracciones de segundo valor es 0*[a]<br /><br /> Valor de datos es válido *valor de marca de tiempo o un valor de hora válido*; fraccionarios parte de segundos es cero [a], [d]<br /><br /> Valor de datos es válido *valor de marca de tiempo*; fraccionarios parte de segundos es distinto de cero [a], [d], [e]<br /><br /> Valor de datos no es válido *valor de hora* o *valor de marca de tiempo*[a]|Datos<br /><br /> Datos<br /><br /> Datos truncados<br /><br /> No definido|6[b]<br /><br /> 6[b]<br /><br /> 6[b]<br /><br /> No definido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIMESTAMP|Valor de datos es válido *valor de marca de tiempo o un valor de hora válido*; fraccionarios parte de los segundos no truncada [a]<br /><br /> Valor de datos es válido *valor de marca de tiempo o un valor de hora válido*; fraccionarios segundos parte truncado [a]<br /><br /> Valor de datos es válido *valor de fecha*[a]<br /><br /> Valor de datos es válido *valor de hora*[a]<br /><br /> Valor de datos no es válido *valor de fecha*, *valor de hora*, o *valor de marca de tiempo*[a]|Datos<br /><br /> Datos truncados<br /><br /> Datos [f]<br /><br /> Datos [g]<br /><br /> No definido|16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> 16[b]<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos los tipos de intervalo de C|Valor de datos es válido *el valor de intervalo*; ningún truncamiento<br /><br /> Valor de datos es válido *el valor de intervalo*; truncamiento de uno o más campos finales<br /><br /> Datos están el intervalo válido; se pierde la precisión significativos campo inicial<br /><br /> El valor de datos no es un valor de intervalo válido|Datos<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
|&nbsp;|&nbsp;|&nbsp;|&nbsp;|&nbsp;|

 [a] el valor de *BufferLength* se omite para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] trata del tamaño del tipo de datos C correspondiente.  
  
 [c] la parte de hora de la *valor de marca de tiempo* se trunca.  
  
 [d] la parte de fecha de la *valor de marca de tiempo* se omite.  
  
 [e] la parte de fracciones de segundos de la marca de tiempo se trunca.  
  
 [f] los campos de tiempo de la estructura de marca de tiempo se establecen en cero.  
  
 [g] los campos de fecha de la estructura de marca de tiempo se establecen en la fecha actual.  

**Espacios adicionales**

Espacios iniciales y finales se omiten cuando los datos de caracteres SQL se convierte en cualquiera de los siguientes tipos:

- Date
- NUMERIC
- time
- TIMESTAMP
- datos de intervalo de C
