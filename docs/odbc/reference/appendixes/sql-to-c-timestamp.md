---
title: 'SQL a C: Marca de tiempo | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 69c9f1258f35a69d6554783f5d1b4ca79be313d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259259"
---
# <a name="sql-to-c-timestamp"></a>SQL a C: Timestamp

El identificador de la marca de tiempo de tipo de datos SQL de ODBC es la siguiente:

- SQL_TYPE_TIMESTAMP  

La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de SQL de la marca de tiempo de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> 20 < = *BufferLength* < = longitud de bytes de caracteres<br /><br /> *BufferLength* < 20|Datos<br /><br /> Datos truncados [b]<br /><br /> No definido|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > longitud de caracteres<br /><br /> 20 < = *BufferLength* < = longitud de caracteres<br /><br /> *BufferLength* < 20|Datos<br /><br /> Datos truncados [b]<br /><br /> No definido|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|Datos<br /><br /> No definido|Longitud de datos en bytes<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Parte de la hora de marca de tiempo es cero [a]<br /><br /> Parte de la hora de marca de tiempo es distinto de cero [a]|Datos<br /><br /> Datos truncados [c]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|Parte de fracciones de marca de tiempo es cero [a]<br /><br /> Parte de fracciones de marca de tiempo es distinto de cero [a]|Datos [d]<br /><br /> Datos truncados [d], [e]|6[f]<br /><br /> 6[f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIMESTAMP|No se trunca la parte fraccionaria de segundos de marca de tiempo [a]<br /><br /> Se trunca la parte fraccionaria de segundos de marca de tiempo [a]|Datos [e]<br /><br /> Datos truncados [e]|16[f]<br /><br /> 16[f]|n/d<br /><br /> 01S07|  

 [a] el valor de *BufferLength* se omite para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] las fracciones de segundos de la marca de tiempo se truncan.  
  
 [c] la parte de hora de la marca de tiempo se trunca.  
  
 [d] la parte de fecha de la marca de tiempo se omite.  
  
 [e] la parte de fracciones de segundos de la marca de tiempo se trunca.  
  
 [f] trata del tamaño del tipo de datos C correspondiente.  

Cuando los datos de SQL de marca de tiempo se convierte en datos de caracteres de C, la cadena resultante tiene el "*aaaa*-*mm*-*dd* *hh* :*mm*:*ss*[.*f...*] "formato, donde se puede usar hasta nueve dígitos de fracciones de segundo. Este formato no se ve afectado por la configuración de país Windows®. (Salvo el separador decimal y fracciones de segundo, todo el formato debe utilizarse, independientemente de la precisión del tipo de datos SQL de marca de tiempo.)
