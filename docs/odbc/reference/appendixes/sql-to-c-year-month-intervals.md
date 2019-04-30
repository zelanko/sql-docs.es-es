---
title: 'SQL a C: Intervalos de mes del año | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], about converting
- data conversions from SQL to C types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
ms.assetid: 1233634b-8214-420f-b872-3b2630105ba4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01af57739f23db586991f8a54d14b90b47f15933
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259574"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL a C: Intervalos de mes y año

Los identificadores de los tipos de datos SQL de ODBC de año y mes intervalo son los siguientes:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

En la tabla siguiente se muestra la C de ODBC para el mes de año el intervalo de datos de SQL se puede convertir los tipos de datos. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo de C|Prueba|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|No se trunca la parte de los campos final<br /><br /> Parte de los campos finales truncado<br /><br /> La precisión de destino inicial no es lo suficientemente grande como para contener los datos de origen|Datos<br /><br /> Datos truncados<br /><br /> No definido|Longitud de datos en bytes<br /><br /> Longitud de datos en bytes<br /><br /> No definido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|Precisión de intervalo era de un solo campo y los datos se convierten sin truncamiento<br /><br /> Precisión de intervalo era de un solo campo y totalmente truncado<br /><br /> Precisión de intervalo no era un solo campo|Datos<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Longitud de datos en bytes<br /><br /> Tamaño del tipo de datos C|n/d<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Longitud de bytes de datos < = *BufferLength*<br /><br /> Longitud de bytes de datos > *BufferLength*|Datos<br /><br /> No definido|Longitud de datos en bytes<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_CHAR|Longitud de bytes de caracteres < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) > = *BufferLength*|Datos<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud de caracteres < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) < *BufferLength*<br /><br /> Número de dígitos de entero (en contraposición a fraccionarios) > = *BufferLength*|Datos<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|n/d<br /><br /> 01004<br /><br /> 22003|  
  
 [a] intervalo de meses del año de un tipo SQL puede convertirse a cualquier tipo de intervalo C año / mes.  
  
 [b] si la precisión de intervalo es un único campo (uno de los años o meses), se puede convertir el intervalo de tipo SQL a cualquier valor numérico exacto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversiones predeterminadas

La conversión predeterminada de un intervalo de tipo SQL es el tipo de datos de intervalo de C correspondiente. La aplicación, a continuación, enlaza la columna o parámetro (o establece el campo SQL_DESC_DATA_PTR en el registro adecuado de la descartar) para que apunte a la estructura SQL_INTERVAL_STRUCT inicializada (o se pasa un puntero a la estructura de SQL_ INTERVAL_STRUCT como el *TargetValuePtr* argumento en una llamada a **SQLGetData**).
