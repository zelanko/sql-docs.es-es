---
title: Campos de descriptor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], fields
- header fields [ODBC]
- record fields [ODBC]
ms.assetid: f38623c8-fdd4-4601-b1f0-97c593d31177
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5025bf5eee4b0b65342e7ce47cbbde4ae9ef6b7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106172"
---
# <a name="descriptor-fields"></a>Campos de descriptor
Los descriptores contienen campos de *encabezado* y *registro* que describen por completo las columnas o los parámetros.  
  
 Un descriptor contiene una única copia de los siguientes campos de encabezado. Cambiar un campo de encabezado afecta a todas las columnas o parámetros.  
  
|||  
|-|-|  
|SQL_DESC_ALLOC_TYPE|SQL_DESC_BIND_TYPE|  
|SQL_DESC_ARRAY_SIZE|SQL_DESC_COUNT|  
|SQL_DESC_ARRAY_STATUS_PTR|SQL_DESC_ROWS_PROCESSED_PTR|  
|SQL_DESC_BIND_OFFSET_PTR||  
  
 Un descriptor contiene cero o más registros de descriptores. Cada registro describe una columna o un parámetro, dependiendo del tipo de descriptor. Cuando se enlaza un nuevo parámetro o columna, se agrega un nuevo registro al descriptor. Cuando una columna o un parámetro no están enlazados, se quita un registro del descriptor. Cada registro contiene una única copia de los siguientes campos:  
  
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
  
 Muchos atributos de instrucción se corresponden con el campo de encabezado de un descriptor. La configuración de estos atributos a través de una llamada a **SQLSetStmtAttr** y el campo correspondiente del encabezado del descriptor llamando a **SQLSetDescField** tienen el mismo efecto. Lo mismo se aplica a **SQLGetStmtAttr** y **SQLGetDescField**, que recuperan la misma información. Llamar a las funciones de instrucción en lugar de las funciones de descriptor tiene la ventaja de que no es necesario recuperar un identificador de descriptor.  
  
 Los campos de encabezado siguientes se pueden establecer mediante el establecimiento de atributos de instrucción:  
  
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
