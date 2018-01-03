---
title: 'SQL hasta la fecha C: | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to C types [ODBC], date
- date data type [ODBC]
- data conversions from SQL to C types [ODBC], date
ms.assetid: 703c7960-9cf4-4d7a-9920-53b29c184f97
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87a62501d4d03073d8c43b2f791ceffeec9b0b30
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sql-to-c-date"></a>SQL hasta la fecha C:
El identificador para el tipo de datos SQL de ODBC date es:  
  
 SQL_TYPE_DATE  
  
 La siguiente tabla muestra los tipos de datos a la que se puede convertir los datos SQL de la fecha de la C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|*BufferLength* > longitud de bytes de caracteres<br /><br /> 11 < = *BufferLength* < = longitud de bytes de caracteres<br /><br /> *BufferLength* < 11|data<br /><br /> Datos truncados<br /><br /> No definido|10<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|*BufferLength* > longitud de caracteres<br /><br /> 11 < = *BufferLength* < = longitud de caracteres<br /><br /> *BufferLength* < 11|data<br /><br /> Datos truncados<br /><br /> No definido|10<br /><br /> Longitud de datos de caracteres<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_TYPE_DATE|Ninguno [a]|data|6 [c]|n/d|  
|SQL_C_TYPE_TIMESTAMP|Ninguno [a]|Datos [b]|16 [c]|n/d|  
  
 [a] el valor de *BufferLength* se pasa por alto para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b], los campos de hora de la estructura de marca de tiempo se establecen en cero.  
  
 [c] es el tamaño del tipo de datos C correspondiente.  
  
 Cuando la fecha de datos de SQL se convierte en datos de caracteres C, la cadena resultante es en el "*aaaa*-*mm*-*dd*" formato. Este formato no se ve afectado por el valor de país Windows®.
