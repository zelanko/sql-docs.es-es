---
title: 'SQL en C: carácter | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], character
- character data type [ODBC]
- data conversions from SQL to C types [ODBC], character
ms.assetid: 7fdb7f38-b64d-48f2-bcb4-1ca96b2bbdb6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d5759b17e0fe306edd5a79a8aa50a5fad9f5f690
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sql-to-c-character"></a>SQL a caracteres C:
Los identificadores para los tipos de datos SQL de ODBC de caracteres son:  
  
 SQL_CHAR  
  
 SQL_VARCHAR  
  
 SQL_LONGVARCHAR  
  
 SQL_WCHAR  
  
 SQL_WVARCHAR  
  
 SQL_WLONGVARCHAR  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de SQL de caracteres de C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Longitud de bytes de datos < *BufferLength*<br /><br /> Longitud de bytes de datos > = *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|Longitud de datos de caracteres < *BufferLength*<br /><br /> Longitud de datos de caracteres > = *BufferLength*|data<br /><br /> Datos truncados|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres|n/d<br /><br /> 01004|  
|SQL_C_STINYINT SQL_C_UTINYINT SQL_C_TINYINT SQL_C_SBIGINT SQL_C_UBIGINT SQL_C_SSHORT SQL_C_USHORT SQL_C_SHORT SQL_C_SLONG SQL_C_ULONG SQL_C_LONG SQL_C_NUMERIC|Los datos se convierten sin truncamiento [b]<br /><br /> Los datos se convierten con el truncamiento de los dígitos fraccionarios [a]<br /><br /> Conversión de datos dé como resultado la pérdida de dígitos enteros (en lugar de fracciones) [a]<br /><br /> Datos no están un *literal numérico*[b].|data<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|Número de bytes del tipo de datos C<br /><br /> Número de bytes del tipo de datos C<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_FLOAT SQL_C_DOUBLE|Datos están dentro del intervalo del tipo de datos a la que se va a convertir el número [a]<br /><br /> Datos están fuera del intervalo del tipo de datos a la que se va a convertir el número [a]<br /><br /> Datos no están un *literal numérico*[b].|data<br /><br /> No definido<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 22003<br /><br /> 22018|  
_C_BIT|Los datos son 0 o 1<br /><br /> Datos están mayores que 0, inferior a 2 y no es igual a 1<br /><br /> Datos están menor que 0 o mayor que o igual a 2<br /><br /> Datos no están un *literal numérico*|data<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|1 [b]<br /><br /> 1 [b]<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22003<br /><br /> 22018|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> Datos truncados|Longitud de los datos en bytes<br /><br /> Longitud de datos|n/d<br /><br /> 01004|  
|SQL_C_TYPE_DATE|Valor de datos es válido *valor de fecha*[a]<br /><br /> Valor de datos es válido *valor timestamp*; parte de hora es cero [a]<br /><br /> Valor de datos es válido *valor timestamp*; parte de hora es distinto de cero [a], [c]<br /><br /> Valor de datos no es válido *valor de fecha* o *valor timestamp*[a]|data<br /><br /> data<br /><br /> Datos truncados<br /><br /> No definido|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> No definido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
|SQL_C_TYPE_TIME|Valor de datos es válido *valor de hora y las fracciones de segundo valor es 0*[a]<br /><br /> Valor de datos es válido *valor timestamp o un valor de hora válido*; fracciones parte de segundos es cero [a], [d]<br /><br /> Valor de datos es válido *valor timestamp*; fracciones parte de segundos es distinto de cero [a], [d] [e]<br /><br /> Valor de datos no es válido *valor de hora* o *valor timestamp*[a]|data<br /><br /> data<br /><br /> Datos truncados<br /><br /> No definido|6 [b]<br /><br /> 6 [b]<br /><br /> 6 [b]<br /><br /> No definido|n/d<br /><br /> n/d<br /><br /> 01S07<br /><br /> 22018|  
_C_TYPE_TIMESTAMP|Valor de datos es válido *valor timestamp o un valor de hora válido*; fracciones segundos parte no truncada [a]<br /><br /> Valor de datos es válido *valor timestamp o un valor de hora válido*; fracciones segundos parte truncado [a]<br /><br /> Valor de datos es válido *valor de fecha*[a]<br /><br /> Valor de datos es válido *valor de hora*[a]<br /><br /> Valor de datos no es válido *valor de fecha*, *valor de hora*, o *valor timestamp*[a]|data<br /><br /> Datos truncados<br /><br /> Datos [f]<br /><br /> Datos [g]<br /><br /> No definido|16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> 16 [b]<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos los tipos de intervalo de C|Valor de datos es válido *el valor del intervalo*; ningún truncamiento<br /><br /> Valor de datos es válido *el valor del intervalo*; truncamiento de uno o más campos finales<br /><br /> Datos están el intervalo válido; se pierde la precisión de campo significativos del principio<br /><br /> El valor de datos no es un valor de intervalo válido|data<br /><br /> Datos truncados<br /><br /> No definido<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015<br /><br /> 22018|  
  
 [a] el valor de *BufferLength* se pasa por alto para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] es el tamaño del tipo de datos C correspondiente.  
  
 [c] la parte de hora de la *valor timestamp* se trunca.  
  
 [d] la parte de la fecha de la *valor timestamp* se omite.  
  
 [e] la parte de las fracciones de segundo de la marca de tiempo se trunca.  
  
 [f], los campos de hora de la estructura de marca de tiempo se establecen en cero.  
  
 [g], los campos de fecha de la estructura de marca de tiempo se establecen en la fecha actual.  
  
 Cuando se convierten datos de SQL de caracteres numéricos, fecha, hora, marca de tiempo o datos de intervalo C, espacios iniciales y finales se omiten.
