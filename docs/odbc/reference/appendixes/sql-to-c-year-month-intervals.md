---
title: "SQL a intervalos de mes y año C: | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4acd46374597b19849abfaa7cb547c8b6af23bd9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sql-to-c-year-month-intervals"></a>SQL a intervalos de meses del año C:
Los identificadores para los tipos de datos SQL de ODBC de intervalo de meses del año son:  
  
 SQL_INTERVAL_YEAR  
  
 SQL_INTERVAL_MONTH  
  
 SQL_INTERVAL_YEAR_TO_MONTH  
  
 En la tabla siguiente se muestra la C de ODBC en qué mes y año-intervalo de datos de SQL se puede convertir los tipos de datos. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH [a]<br /><br /> SQL_C_INTERVAL_YEAR [a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH [a]|No se trunca la parte campos final<br /><br /> Parte de campos finales truncado<br /><br /> Precisión de destino del principio no es lo suficientemente grande como para contener los datos de origen|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT [b]<br /><br /> SQL_C_UTINYINT [b]<br /><br /> SQL_C_USHORT [b]<br /><br /> SQL_C_SHORT [b]<br /><br /> SQL_C_SLONG [b]<br /><br /> SQL_C_ULONG [b]<br /><br /> SQL_C_NUMERIC [b]<br /><br /> SQL_C_BIGINT [b]|Precisión de intervalo era de un solo campo y los datos se convierten sin truncamiento<br /><br /> Precisión de intervalo era de un único campo y todo truncado<br /><br /> Precisión de intervalo no era un campo único|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Longitud de los datos en bytes<br /><br /> Tamaño del tipo de datos C|n/d<br /><br /> 22003<br /><br /> 22015|  
_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Longitud de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) > = *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (en lugar de fracciones) > = *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de meses del año de un tipo de SQL se puede convertir a cualquier tipo de intervalo C-mes y año.  
  
 [b] si la precisión de intervalo es un campo único (uno del año o mes), se puede convertir el tipo SQL de intervalo para cualquier valor numérico exacto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  
  
 La conversión de valor predeterminado de un intervalo de tipo SQL es el tipo de datos de intervalo de C correspondiente. La aplicación, a continuación, enlaza la columna o parámetro (o establece el campo SQL_DESC_DATA_PTR en el registro adecuado de la descartar) para que apunte a la estructura SQL_INTERVAL_STRUCT inicializada (o se pasa un puntero a la estructura de SQL_ INTERVAL_STRUCT como el *TargetValuePtr* argumento en una llamada a **SQLGetData**).
