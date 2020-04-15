---
title: 'SQL a C: Intervalos de año-mes ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba79a4d6165a43676634a6b79db56b88f5bcc234
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296395"
---
# <a name="sql-to-c-year-month-intervals"></a>SQL a C: Intervalos de mes y año

Los identificadores para los tipos de datos SQL ODBC de intervalo de año-mes son los siguientes:

- SQL_INTERVAL_MONTH
- SQL_INTERVAL_YEAR
- SQL_INTERVAL_YEAR_TO_MONTH

En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir los datos SQL de intervalo de un año-mes. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  

|Identificador de tipo C|Prueba|TargetValuePtr|StrLen_or_IndPtr|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_INTERVAL_MONTH[a]<br /><br /> SQL_C_INTERVAL_YEAR[a]<br /><br /> SQL_C_INTERVAL_YEAR_TO_MONTH[a]|Parte de los campos finales no truncada<br /><br /> Parte de los campos finales truncada<br /><br /> La precisión principal del objetivo no es lo suficientemente grande como para contener datos del origen|data<br /><br /> Datos truncados<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_STINYINT[b]<br /><br /> SQL_C_UTINYINT[b]<br /><br /> SQL_C_USHORT[b]<br /><br /> SQL_C_SHORT[b]<br /><br /> SQL_C_SLONG[b]<br /><br /> SQL_C_ULONG[b]<br /><br /> SQL_C_NUMERIC[b]<br /><br /> SQL_C_BIGINT[b]|La precisión del intervalo era un solo campo y los datos se convirtieron sin truncamiento<br /><br /> La precisión del intervalo era un solo campo y se truncaba todo<br /><br /> La precisión del intervalo no era un solo campo|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Longitud de los datos en bytes<br /><br /> Tamaño del tipo de datos C|N/D<br /><br /> 22003<br /><br /> 22015|  
|SQL_C_BINARY|Longitud de bytes de los datos <- *BufferLength*<br /><br /> Longitud de bytes de los datos > *BufferLength*|data<br /><br /> No definido|Longitud de los datos en bytes<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_CHAR|Longitud de byte de caracteres < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) >- *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Longitud del carácter < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) < *BufferLength*<br /><br /> Número de dígitos enteros (a diferencia de los fracciones) >- *BufferLength*|data<br /><br /> Datos truncados<br /><br /> No definido|Tamaño del tipo de datos C<br /><br /> Tamaño del tipo de datos C<br /><br /> No definido|N/D<br /><br /> 01004<br /><br /> 22003|  
  
 [a] Un tipo SQL de intervalo de año-mes se puede convertir a cualquier tipo de intervalo C de mes de año.  
  
 [b] Si la precisión del intervalo es un solo campo (uno de YEAR o MONTH), el tipo SQL de intervalo se puede convertir en cualquier número exacto (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_USHORT, SQL_C_SHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC).  

## <a name="default-conversions"></a>Conversiones predeterminadas

La conversión predeterminada de un tipo SQL de intervalo es al tipo de datos de intervalo C correspondiente. A continuación, la aplicación enlaza la columna o parámetro (o establece el campo SQL_DESC_DATA_PTR en el registro adecuado de la ARD) para que apunte a la estructura de SQL_INTERVAL_STRUCT inicializada (o pasa un puntero a la estructura INTERVAL_STRUCT SQL_ como el *TargetValuePtr* argumento en una llamada a **SQLGetData**).
