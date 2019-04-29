---
title: Conformidad de campo descriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 193bdadaf36e975b1f79327bfef161daaaed427b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049856"
---
# <a name="descriptor-field-conformance"></a>Conformidad de campo de descriptor
En la tabla siguiente indica el nivel de cumplimiento de cada campo de encabezado de descriptor ODBC, donde esto está bien definido.  
  
|Función|nivel de cumplimiento|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|Base (para APD, DPI y IRD); Nivel 1 (para descartar)|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 En la tabla siguiente indica el nivel de cumplimiento de cada campo de registro del descriptor ODBC, donde esto está bien definido.  
  
|Función|nivel de cumplimiento|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nivel 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|Nivel 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|Nivel 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|SQL_DESC_DATETIME_INTERVAL_ CODE|Core [1]|  
|SQL_DESC_DATETIME_INTERVAL_ PRECISION|Core [1]|  
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
|SQL_DESC_PARAMETER_TYPE|Core/nivel 2 [2]|  
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
  
 [1] compatibilidad para estos campos de registro solo es necesario si el controlador admite los tipos de datos aplicable.  
  
 [2] para el acuerdo de nivel básico, el controlador debe admitir SQL_PARAM_INPUT. Para el cumplimiento de la interfaz de nivel 2, también debe admitir el controlador SQL_PARAM_INPUT_OUTPUT y SQL_PARAM_OUTPUT.
