---
title: 'SQL a la marca de tiempo C: | Documentos de Microsoft'
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
ms.topic: conceptual
helpviewer_keywords:
- timestamp data type [ODBC]
- converting data from SQL to C types [ODBC], timestamp
- data conversions from SQL to C types [ODBC], timestamp
ms.assetid: 6a0617cf-d8c0-4316-8bb4-e6ddb45d7bf1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f3ace8f40ecafc857c63dca58ec072247d3b475
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-timestamp"></a>SQL a la marca de tiempo C:
El identificador de la marca de tiempo de tipo de datos SQL de ODBC es:  
  
 SQL_TYPE_TIMESTAMP  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos SQL de marca de tiempo de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> 20 < = *BufferLength* < = longitud de bytes de caracteres<br /><br /> *BufferLength* < 20|data<br /><br /> Datos truncados [b]<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > longitud de caracteres<br /><br /> 20 < = *BufferLength* < = longitud de caracteres<br /><br /> *BufferLength* < 20|data<br /><br /> Datos truncados [b]<br /><br /> No definido|Longitud de datos de caracteres<br /><br /> Longitud de datos de caracteres<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Parte de hora de marca de tiempo es cero [a]<br /><br /> Parte de hora de marca de tiempo es distinto de cero [a]|data<br /><br /> Datos truncados [c]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
|SQL_C_TYPE_TIME|Parte de las fracciones de segundo de marca de tiempo es cero [a]<br /><br /> Parte de las fracciones de segundo de marca de tiempo es distinto de cero [a]|Datos [d]<br /><br /> Datos truncados [d], [e]|6 [f]<br /><br /> 6 [f]|n/d<br /><br /> 01S07|  
_C_TYPE_TIMESTAMP|No se trunca la parte de las fracciones de segundo de marca de tiempo [a]<br /><br /> Se trunca la parte de las fracciones de segundo de marca de tiempo [a]|Datos [e]<br /><br /> Datos truncados [e]|16 [f]<br /><br /> 16 [f]|n/d<br /><br /> 01S07|  
  
 [a] el valor de *BufferLength* se pasa por alto para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] las fracciones de segundo de la marca de tiempo se truncan.  
  
 [c] la parte de hora de la marca de tiempo se trunca.  
  
 [d] se omite la parte de la fecha de la marca de tiempo.  
  
 [e] la parte de las fracciones de segundo de la marca de tiempo se trunca.  
  
 [f] es el tamaño del tipo de datos C correspondiente.  
  
 Cuando los datos de SQL de marca de tiempo se convierte en datos de caracteres C, la cadena resultante es en el "*aaaa*-*mm*-*dd* *hh* :*mm*:*ss*[.*f...*] "formato, donde puede usarse hasta nueve dígitos de fracciones de segundo. Este formato no se ve afectado por el valor de país Windows®. (Salvo el separador decimal y fracciones de segundo, todo el formato debe utilizarse, independientemente de la precisión del tipo de datos SQL de marca de tiempo.)
