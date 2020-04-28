---
title: Conformidad del campo descriptor | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce33adfdbfceef56936b22c549b6762521b4798
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305936"
---
# <a name="descriptor-field-conformance"></a>Conformidad de campo de descriptor
En la tabla siguiente se indica el nivel de cumplimiento de cada campo de encabezado de descriptor ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Principal|  
|SQL_DESC_ARRAY_SIZE|Principal|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (para APD, DPI y IRD); Nivel 1 (para ARD)|  
|SQL_DESC_BIND_OFFSET_PTR|Principal|  
|SQL_DESC_BIND_TYPE|Principal|  
|SQL_DESC_COUNT|Principal|  
|SQL_DESC_ROWS_PROCESSED_PTR|Principal|  
  
 En la tabla siguiente se indica el nivel de cumplimiento de cada campo de registro del descriptor de ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nivel 2|  
|SQL_DESC_BASE_COLUMN_NAME|Principal|  
|SQL_DESC_BASE_TABLE_NAME|Nivel 1|  
|SQL_DESC_CASE_SENSITIVE|Principal|  
|SQL_DESC_CATALOG_NAME|Nivel 2|  
|SQL_DESC_CONCISE_TYPE|Principal|  
|SQL_DESC_DATA_PTR|Principal|  
|CÓDIGO DE SQL_DESC_DATETIME_INTERVAL_|Núcleo [1]|  
|PRECISIÓN DE SQL_DESC_DATETIME_INTERVAL_|Núcleo [1]|  
|SQL_DESC_DISPLAY_SIZE|Principal|  
|SQL_DESC_FIXED_PREC_SCALE|Principal|  
|SQL_DESC_INDICATOR_PTR|Principal|  
|SQL_DESC_LABEL|Nivel 2|  
|SQL_DESC_LENGTH|Principal|  
|SQL_DESC_LITERAL_PREFIX|Principal|  
|SQL_DESC_LITERAL_SUFFIX|Principal|  
|SQL_DESC_LOCAL_TYPE_NAME|Principal|  
|SQL_DESC_NAME|Principal|  
|SQL_DESC_NULLABLE|Principal|  
|SQL_DESC_OCTET_LENGTH|Principal|  
|SQL_DESC_OCTET_LENGTH_PTR|Principal|  
|SQL_DESC_PARAMETER_TYPE|Núcleo/nivel 2 [2]|  
|SQL_DESC_PRECISION|Principal|  
|SQL_DESC_ROWVER|Nivel 1|  
|SQL_DESC_SCALE|Principal|  
|SQL_DESC_SCHEMA_NAME|Nivel 1|  
|SQL_DESC_SEARCHABLE|Principal|  
|SQL_DESC_TABLE_NAME|Nivel 1|  
|SQL_DESC_TYPE|Principal|  
|SQL_DESC_TYPE_NAME|Principal|  
|SQL_DESC_UNNAMED|Principal|  
|SQL_DESC_UNSIGNED|Principal|  
|SQL_DESC_UPDATABLE|Principal|  
  
 [1] la compatibilidad con estos campos de registro solo es necesaria si el controlador admite los tipos de datos aplicables.  
  
 [2] para la conformidad de nivel básico, el controlador debe admitir SQL_PARAM_INPUT. En el caso del cumplimiento de la interfaz de nivel 2, el controlador también debe admitir SQL_PARAM_INPUT_OUTPUT y SQL_PARAM_OUTPUT.
