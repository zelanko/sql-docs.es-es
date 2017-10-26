---
title: Campos de descriptor | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 014a79813f5755e422b5e854b98f737d59a280a6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-fields"></a>Campos de descriptor
Los descriptores de contienen *encabezado* y *registro* campos que describen completamente columnas o parámetros.  
  
 Un descriptor de contiene una única copia de los siguientes campos de encabezado. Cambiar un campo de cabecera afecta a todas las columnas o parámetros.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Un descriptor contiene cero o más registros de descriptor. Cada registro describe una columna o parámetro, según el tipo de descriptor. Cuando se enlaza una nueva columna o parámetro, se agrega un nuevo registro para el descriptor. Cuando una columna o parámetro no está enlazada, se quita un registro del descriptor. Cada registro contiene una única copia de los campos siguientes:  
  
|||  
|-|-|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_DESC_LOCAL_TYPE_NAME|  
|SQL_DESC_BASE_COLUMN_NAME|SQL_DESC_NAME|  
|SQL_DESC_BASE_TABLE_NAME|SQL_DESC_NULLABLE|  
|SQL_DESC_CASE_SENSITIVE|SQL_DESC_OCTET_LENGTH|  
|SQL_DESC_CATALOG_NAME|SQL_DESC_OCTET_LENGTH_PTR|  
|SQL_DESC_CONCISE_TYPE|SQL_DESC_PARAMETER_TYPE|  
|SQL_DESC_DATA_PTR|SQL_DESC_PRECISION|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQL_DESC_SCALE|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQL_DESC_SCHEMA_NAME|  
|SQL_DESC_DISPLAY_SIZE|SQL_DESC_SEARCHABLE|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_DESC_TABLE_NAME|  
|SQL_DESC_INDICATOR_PTR|SQL_DESC_TYPE|  
|SQL_DESC_LABEL|SQL_DESC_TYPE_NAME|  
|SQL_DESC_LENGTH|SQL_DESC_UNNAMED|  
|SQL_DESC_LITERAL_PREFIX|SQL_DESC_UNSIGNED|  
|SQL_DESC_LITERAL_SUFFIX|SQL_DESC_UPDATABLE|  
  
 Muchos de los atributos de instrucción se corresponden con el campo de encabezado de un descriptor. Establecer estos atributos a través de una llamada a **SQLSetStmtAttr** y establecer el campo de encabezado de descriptor correspondiente mediante una llamada a **SQLSetDescField** tienen el mismo efecto. Lo mismo puede decirse de **SQLGetStmtAttr** y **SQLGetDescField**, lo cual recuperan la misma información. Al llamar a las funciones de instrucción en lugar de las funciones de descriptor tiene la ventaja de que no tiene un identificador de descriptor va a recuperar.  
  
 Los siguientes campos de encabezado pueden establecerse mediante el establecimiento de atributos de instrucción:  
  
|||  
|-|-|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Esta sección contiene los temas siguientes.  
  
-   [Número de registros](../../../odbc/reference/develop-app/record-count.md)  
  
-   [Registros de Descriptor de enlace](../../../odbc/reference/develop-app/bound-descriptor-records.md)  
  
-   [Campos aplazados](../../../odbc/reference/develop-app/deferred-fields.md)  
  
-   [Comprobación de coherencia](../../../odbc/reference/develop-app/consistency-check.md)

