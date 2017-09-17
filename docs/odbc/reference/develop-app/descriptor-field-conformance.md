---
title: Conformidad de campo descriptor | Documentos de Microsoft
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
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 049208450144fdd1c1d3b902093517627486ccf9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-field-conformance"></a>Conformidad de campo de descriptor
En la tabla siguiente indica el nivel de conformidad de cada campo de encabezado de descriptor ODBC, donde esto está bien definido.  
  
|Función|Nivel de conformidad|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|Base (para APD, DPI y IRD); Nivel 1 (para descartar)|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 En la tabla siguiente indica el nivel de conformidad de cada campo de registro del descriptor ODBC, donde esto está bien definido.  
  
|Función|Nivel de conformidad|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nivel 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|Nivel 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|Nivel 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|CÓDIGO DE SQL_DESC_DATETIME_INTERVAL_|Core [1]|  
|PRECISIÓN DE SQL_DESC_DATETIME_INTERVAL_|Core [1]|  
|SQL_DESC_DISPLAY_SIZE|Core|  
|SQL_DESC_FIXED_PREC_SCALE|Core|  
|SQL_DESC_INDICATOR_PTR|Core|  
|SQL_DESC_LABEL|Nivel 2|  
|SQL_DESC_LENGTH|Core|  
|SQL_DESC_LITERAL_PREFIX|Core|  
|SQL_DESC_LITERAL_SUFFIX|Core|  
|SQL_DESC_LOCAL_TYPE_NAME|Core|  
|SQL_DESC_NAME|Core|  
|SQL_DESC_NULLABLE|Core|  
|SQL_DESC_OCTET_LENGTH|Core|  
|SQL_DESC_OCTET_LENGTH_PTR|Core|  
|SQL_DESC_PARAMETER_TYPE|Nivel de núcleo/2 [2]|  
|SQL_DESC_PRECISION|Core|  
|SQL_DESC_ROWVER|Nivel 1|  
|SQL_DESC_SCALE|Core|  
|SQL_DESC_SCHEMA_NAME|Nivel 1|  
|SQL_DESC_SEARCHABLE|Core|  
|SQL_DESC_TABLE_NAME|Nivel 1|  
|SQL_DESC_TYPE|Core|  
|SQL_DESC_TYPE_NAME|Core|  
|SQL_DESC_UNNAMED|Core|  
|SQL_DESC_UNSIGNED|Core|  
|SQL_DESC_UPDATABLE|Core|  
  
 [1] soporte técnico para estos campos de registro sólo es necesario si el controlador es compatible con los tipos de datos es aplicable.  
  
 [2] para el acuerdo de nivel de núcleo, el controlador debe admitir SQL_PARAM_INPUT. Para el cumplimiento de la interfaz de nivel 2, el controlador también debe admitir SQL_PARAM_INPUT_OUTPUT y SQL_PARAM_OUTPUT.
