---
title: 'SQL a C: Date | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe0c30f0f0fbf0ea695d79387fdec3694a54ebca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151272"
---
# <a name="sql-to-c-date"></a>SQL a C: date
El identificador de tipo de datos SQL de ODBC date es:  
  
 SQL_TYPE_DATE  
  
 La siguiente tabla muestra los tipos de datos a la que se puede convertir los datos SQL de la fecha de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> 11 < = *BufferLength* < = longitud de bytes de caracteres<br /><br /> *BufferLength* < 11|Datos<br /><br /> Datos truncados<br /><br /> No definido|10<br /><br /> Longitud de datos en bytes<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > longitud de caracteres<br /><br /> 11 < = *BufferLength* < = longitud de caracteres<br /><br /> *BufferLength* < 11|Datos<br /><br /> Datos truncados<br /><br /> No definido|10<br /><br /> Longitud de datos de caracteres<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|Datos<br /><br /> No definido|Longitud de datos en bytes<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|[A] ninguno|Datos|6[c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|[A] ninguno|Datos [b]|16[c]|n/d|  
  
 [a] el valor de *BufferLength* se omite para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] los campos de tiempo de la estructura de marca de tiempo se establecen en cero.  
  
 [c] trata del tamaño del tipo de datos C correspondiente.  
  
 Cuando la fecha de datos de SQL se convierte en datos de caracteres de C, la cadena resultante tiene el "*aaaa*-*mm*-*dd*" formato. Este formato no se ve afectado por la configuración de país Windows®.
