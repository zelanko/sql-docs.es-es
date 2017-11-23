---
title: Atributo conformidad | Documentos de Microsoft
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
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
- conformance levels [ODBC], attribute
- attribute conformance levels [ODBC]
ms.assetid: 34fea100-10f9-46d5-bc50-3aa867b70f24
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7859fbb5483acd09dd99f4f27be77d5874e7b992
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="attribute-conformance"></a>Conformidad de atributo
En la tabla siguiente indica el nivel de conformidad de cada atributo de entorno de ODBC, donde esto está bien definido.  
  
|Función|Nivel de conformidad|  
|--------------|-----------------------|  
|SQL_ATTR_CONNECTION_POOLING|--[1]|  
|SQL_ATTR_CP_MATCH|--[1]|  
|SQL_ATTR_ODBC_VER|Core|  
|SQL_ATTR_OUTPUT_NTS|--[1]|  
  
 [1] ésta es una característica opcional y por lo tanto no forma parte de los niveles de cumplimiento.  
  
 En la tabla siguiente indica el nivel de conformidad de cada atributo de conexión ODBC, donde esto está bien definido.  
  
|Función|Nivel de conformidad|  
|--------------|-----------------------|  
|SQL_ATTR_ACCESS_MODE|Core|  
|SQL_ATTR_ASYNC_ENABLE|Nivel 1 o nivel 2 [1]|  
|SQL_ATTR_AUTO_IPD|Nivel 2|  
|SQL_ATTR_AUTOCOMMIT|Nivel 1|  
|SQL_ATTR_CONNECTION_DEAD|Nivel 1|  
|SQL_ATTR_CONNECTION_TIMEOUT|Nivel 2|  
|SQL_ATTR_CURRENT_CATALOG|Nivel 2|  
|SQL_ATTR_LOGIN_TIMEOUT|Nivel 2|  
|SQL_ATTR_ODBC_CURSORS|Core|  
|SQL_ATTR_PACKET_SIZE|Nivel 2|  
|SQL_ATTR_QUIET_MODE|Core|  
|SQL_ATTR_TRACE|Core|  
|SQL_ATTR_TRACEFILE|Core|  
|SQL_ATTR_TRANSLATE_LIB|Core|  
|SQL_ATTR_TRANSLATE_OPTION|Core|  
|SQL_ATTR_TXN_ISOLATION|Nivel 1 o nivel 2 [2]|  
  
 [1] las aplicaciones que admiten la asincronía de nivel de conexión (necesaria para el nivel 1) deben admitir establecer este atributo en SQL_TRUE mediante una llamada a **SQLSetConnectAttr**; el atributo no tienen que ser puede establecer en un valor distinto del predeterminado valor a través de **SQLSetStmtAttr**. Las aplicaciones que admiten la asincronía de nivel de instrucción (requerida para el nivel 2) deben admitir establecer este atributo en SQL_TRUE con cualquier función.  
  
 [2] para el acuerdo de la interfaz de nivel 1, el controlador debe admitir un valor además del valor predeterminado definido por el controlador (disponible mediante una llamada a **SQLGetInfo** con la opción SQL_DEFAULT_TXN_ISOLATION). Para el cumplimiento de la interfaz de nivel 2, el controlador también debe admitir SQL_TXN_SERIALIZABLE.  
  
 En la tabla siguiente indica el nivel de conformidad de cada atributo de instrucción ODBC, donde esto está bien definido.  
  
|Función|Nivel de conformidad|  
|--------------|-----------------------|  
|SQL_ATTR_APP_PARAM_DESC|Core|  
|SQL_ATTR_APP_ROW_DESC|Core|  
|SQL_ATTR_ASYNC_ENABLE|Nivel 1 o nivel 2 [1]|  
|SQL_ATTR_CONCURRENCY|Nivel 1 o nivel 2 [2]|  
|SQL_ATTR_CURSOR_SCROLLABLE|Nivel 1|  
|SQL_ATTR_CURSOR_SENSITIVITY|Nivel 2|  
|SQL_ATTR_CURSOR_TYPE|Nivel de núcleo/2 [3]|  
|SQL_ATTR_ENABLE_AUTO_IPD|Nivel 2|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|Nivel 2|  
|SQL_ATTR_IMP_PARAM_DESC|Core|  
|SQL_ATTR_IMP_ROW_DESC|Core|  
|SQL_ATTR_KEYSET_SIZE|Nivel 2|  
|SQL_ATTR_MAX_LENGTH|Nivel 1|  
|SQL_ATTR_MAX_ROWS|Nivel 1|  
|SQL_ATTR_METADATA_ID|Core|  
|SQL_ATTR_NOSCAN|Core|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_PARAM_BIND_TYPE|Core|  
|SQL_ATTR_PARAM_OPERATION_PTR|Core|  
|SQL_ATTR_PARAM_STATUS_PTR|Core|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|Core|  
|SQL_ATTR_PARAMSET_SIZE|Core|  
|SQL_ATTR_QUERY_TIMEOUT|Nivel 2|  
|SQL_ATTR_RETRIEVE_DATA|Nivel 1|  
|SQL_ATTR_ROW_ARRAY_SIZE|Core|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|Core|  
|SQL_ATTR_ROW_BIND_TYPE|Core|  
|SQL_ATTR_ROW_NUMBER|Nivel 1|  
|SQL_ATTR_ROW_OPERATION_PTR|Nivel 1|  
|SQL_ATTR_ROW_STATUS_PTR|Core|  
|SQL_ATTR_ROWS_FETCHED_PTR|Core|  
|SQL_ATTR_SIMULATE_CURSOR|Nivel 2|  
|SQL_ATTR_USE_BOOKMARKS|Nivel 2|  
  
 [1] las aplicaciones que admiten la asincronía de nivel de conexión (necesaria para el nivel 1) deben admitir establecer este atributo en SQL_TRUE mediante una llamada a **SQLSetConnectAttr**; el atributo no tienen que ser puede establecer en un valor distinto del predeterminado valor a través de **SQLSetStmtAttr**. Las aplicaciones que admiten la asincronía de nivel de instrucción (requerida para el nivel 2) deben admitir establecer este atributo en SQL_TRUE con cualquier función.  
  
 [2] para el acuerdo de la interfaz de nivel 2, el controlador debe admitir SQL_CONCUR_READ_ONLY y al menos otro valor.  
  
 [3] para la conformidad de la interfaz de nivel 1, el controlador debe admitir SQL_CURSOR_FORWARD_ONLY y al menos otro valor. Para el cumplimiento de la interfaz de nivel 2, el controlador debe admitir todos los valores definidos en este documento.
