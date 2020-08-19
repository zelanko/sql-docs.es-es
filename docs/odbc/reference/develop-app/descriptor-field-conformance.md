---
description: Conformidad de campo de descriptor
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
ms.openlocfilehash: 36687cf456f4fcbbaa3f4b029e51098815dec3f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476747"
---
# <a name="descriptor-field-conformance"></a>Conformidad de campo de descriptor
En la tabla siguiente se indica el nivel de cumplimiento de cada campo de encabezado de descriptor ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|Core|  
|SQL_DESC_ARRAY_SIZE|Core|  
|SQL_DESC_ARRAY_STATUS_PTR|Core (para APD, DPI y IRD); Nivel 1 (para ARD)|  
|SQL_DESC_BIND_OFFSET_PTR|Core|  
|SQL_DESC_BIND_TYPE|Core|  
|SQL_DESC_COUNT|Core|  
|SQL_DESC_ROWS_PROCESSED_PTR|Core|  
  
 En la tabla siguiente se indica el nivel de cumplimiento de cada campo de registro del descriptor de ODBC, donde está bien definido.  
  
|Función|Nivel de cumplimiento|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Nivel 2|  
|SQL_DESC_BASE_COLUMN_NAME|Core|  
|SQL_DESC_BASE_TABLE_NAME|Nivel 1|  
|SQL_DESC_CASE_SENSITIVE|Core|  
|SQL_DESC_CATALOG_NAME|Nivel 2|  
|SQL_DESC_CONCISE_TYPE|Core|  
|SQL_DESC_DATA_PTR|Core|  
|CÓDIGO DE SQL_DESC_DATETIME_INTERVAL_|Núcleo [1]|  
|PRECISIÓN DE SQL_DESC_DATETIME_INTERVAL_|Núcleo [1]|  
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
|SQL_DESC_PARAMETER_TYPE|Núcleo/nivel 2 [2]|  
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
  
 [1] la compatibilidad con estos campos de registro solo es necesaria si el controlador admite los tipos de datos aplicables.  
  
 [2] para la conformidad de nivel básico, el controlador debe admitir SQL_PARAM_INPUT. En el caso del cumplimiento de la interfaz de nivel 2, el controlador también debe admitir SQL_PARAM_INPUT_OUTPUT y SQL_PARAM_OUTPUT.
