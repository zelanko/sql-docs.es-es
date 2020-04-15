---
title: 'SQL a C: Fecha ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe9656c0c02c0ff5a10029525da3d38280530cc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296535"
---
# <a name="sql-to-c-date"></a>SQL a C: Date
El identificador del tipo de datos SQL ODBC de fecha es:  
  
 SQL_TYPE_DATE  
  
 En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir los datos SQL de fecha. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  
  
|Identificador de tipo C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> 11 <*de* búfer<de longitud de caracteres de caracteres<br /><br /> *BufferLength* < 11|data<br /><br /> Datos truncados<br /><br /> No definido|10<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > Longitud de caracteres<br /><br /> 11 <*de* búfer<de longitud de búfer de longitud de caracteres<br /><br /> *BufferLength* < 11|data<br /><br /> Datos truncados<br /><br /> No definido|10<br /><br /> Longitud de los datos en caracteres<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Ninguno[a]|data|6[c]|N/D|  
|SQL_C_TYPE_TIMESTAMP|Ninguno[a]|Datos[b]|16[c]|N/D|  
  
 [a] El valor de *BufferLength* se omite para esta conversión. El controlador supone que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] Los campos de tiempo de la estructura de marca de tiempo se establecen en cero.  
  
 [c] Este es el tamaño del tipo de datos C correspondiente.  
  
 Cuando los datos SQL de fecha se convierten en datos de caracteres C, la cadena resultante está en el formato "*aaaa*-*mm*-*dd*". Este formato no se ve afectado por la configuración de país ® de Windows.
