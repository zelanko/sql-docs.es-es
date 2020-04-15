---
title: 'SQL a C: Marca de tiempo ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 552bab585e4480fd922c9b9a6b112830f5c11ad9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296355"
---
# <a name="sql-to-c-timestamp"></a>SQL a C: Timestamp

El identificador del tipo de datos SQL ODBC de marca de tiempo es el siguiente:

- SQL_TYPE_TIMESTAMP  

En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir los datos SQL de marca de tiempo. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  

|Identificador de tipo C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> 20 <de *búferdes <* de caracteres de caracteres<br /><br /> *BufferLength* < 20|data<br /><br /> Datos truncados[b]<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > Longitud de caracteres<br /><br /> 20 <*de* búfer<de longitud de caracteres de la longitud del carácter<br /><br /> *BufferLength* < 20|data<br /><br /> Datos truncados[b]<br /><br /> No definido|Longitud de los datos en caracteres<br /><br /> Longitud de los datos en caracteres<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_TYPE_DATE|La parte de tiempo de la marca de tiempo es cero[a]<br /><br /> La parte de tiempo de la marca de tiempo es distinta de cero[a]|data<br /><br /> Datos truncados[c]|6[f]<br /><br /> 6[f]|N/D<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|La porción de fracciones de segundos de la marca de tiempo es cero[a]<br /><br /> La porción de fracciones de segundos de la marca de tiempo es distinta de cero[a]|Datos[d]<br /><br /> Datos truncados[d], [e]|6[f]<br /><br /> 6[f]|N/D<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|La porción de fracciones de segundo de la marca de tiempo no se trunca[a]<br /><br /> La parte de fracciones de segundo de la marca de tiempo se trunca[a]|Datos[e]<br /><br /> Datos truncados[e]|16[f]<br /><br /> 16[f]|N/D<br /><br /> 01S07|  

 [a] El valor de *BufferLength* se omite para esta conversión. El controlador supone que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] Las fracciones de segundo de la marca de tiempo se truncan.  
  
 [c] La parte de tiempo de la marca de tiempo se trunca.  
  
 [d] Se omite la parte de fecha de la marca de tiempo.  
  
 [e] La parte de fracciones de segundo de la marca de tiempo se trunca.  
  
 [f] Este es el tamaño del tipo de datos C correspondiente.  

Cuando los datos SQL de marca de tiempo se convierten en datos de caracteres C, la cadena resultante se encuentra en el "*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*]" formato, donde se pueden utilizar hasta nueve dígitos durante fracciones de segundo. Este formato no se ve afectado por la configuración de país ® de Windows. (Excepto para el punto decimal y los segundos fraccionarios, se debe utilizar todo el formato, independientemente de la precisión del tipo de datos SQL de marca de tiempo.)
