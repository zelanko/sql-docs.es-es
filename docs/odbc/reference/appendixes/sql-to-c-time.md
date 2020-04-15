---
title: 'SQL a C: Tiempo ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], time
- time data type [ODBC]
- data conversions from SQL to C types [ODBC], time
ms.assetid: 6dc59973-7bb5-40f1-87c8-5bf68b3bf2ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ebd146abf650861099a40bf91b2641df768b343d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296385"
---
# <a name="sql-to-c-time"></a>SQL a C: Time
El identificador para el tipo de datos SQL ODBC de tiempo es:  
  
 SQL_TYPE_TIME  
  
 En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir los datos SQL de tiempo. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  
  
|Identificador de tipo C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> *9* <= *<de longitud de búfer* : Longitud de byte de caracteres<br /><br /> *BufferLength* < 9|data<br /><br /> Datos truncados[a]<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > Longitud de caracteres<br /><br /> *9* <= *Longitud de búfer* <de caracteres de caracteres<br /><br /> *BufferLength* < 9|data<br /><br /> Datos truncados[a]<br /><br /> No definido|Longitud de los datos en caracteres<br /><br /> Longitud de los datos en caracteres<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_TYPE_TIME|Ninguno[b]|data|6[d]|N/D|  
|SQL_C_TYPE_TIMESTAMP|Ninguno[b]|Datos[c]|16[d]|N/D|  
  
 [a] Las fracciones de segundo del tiempo se truncan.  
  
 [b] El valor de *BufferLength* se omite para esta conversión. El controlador supone que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [c] Los campos de fecha de la estructura de marca de tiempo se establecen en la fecha actual y el campo de fracciones de segundo de la estructura de marca de tiempo se establece en cero.  
  
 [d] Este es el tamaño del tipo de datos C correspondiente.  
  
 Cuando los datos SQL de tiempo se convierten en datos de caracteres C, la cadena resultante está en el formato "*hh*:*mm*:*ss*". Este formato no se ve afectado por la configuración de país ® de Windows.
