---
title: Nuevas características ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], new features in release
- ODBC drivers [ODBC], backward compatibility
- new features [ODBC]
- compatibility [ODBC], new features in release
- ODBC [ODBC], new features
ms.assetid: a8fcdd00-6cb3-4871-9489-6018b3d0d65f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b40803dac6c9f296043a8dcac50f9bc69036875a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302403"
---
# <a name="new-features"></a>Características nuevas
La siguiente nueva funcionalidad se ha introducido en ODBC *3.x*. Una aplicación ODBC *3.x* que trabaje con un controlador ODBC *2.x* no podrá utilizar esta funcionalidad. El Administrador de controladores ODBC *3.x* no asigna estas características cuando se trabaja con un controlador ODBC *2.x.*  
  
-   Funciones que toman un identificador de descriptor como argumento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**y **SQLCopyDesc**.  
  
-   Las funciones **SQLSetEnvAttr** y **SQLGetEnvAttr**.  
  
-   El uso de **SQLAllocHandle** para asignar un identificador de descriptor. (El uso de **SQLAllocHandle** para asignar identificadores de entorno, conexión e instrucción se duplica, no es nuevo, funcionalidad.)  
  
-   El uso de **SQLGetConnectAttr** para obtener los atributos de conexión SQL_ATTR_AUTO_IPD. (El uso de **SQLSetConnectAttr** para establecer y **SQLGetConnectAttr** para obtener, otros atributos de conexión se duplica, no nuevo, funcionalidad.)  
  
-   El uso de **SQLSetStmtAttr** para establecer y **SQLGetStmtAttr** para obtener, los siguientes atributos de instrucción. (El uso de **SQLSetStmtAttr** para establecer y **SQLGetStmtAttr** para obtener, otros atributos de instrucción se duplica, no nuevo, funcionalidad.)  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_ENABLE_AUTO_IPD  
  
     SQL_ATTR_FETCH_BOOKMARK_PTR  
  
     SQL_ATTR_BIND_OFFSET  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     SQL_DESC_PARAM_STATUS_PTR  
  
     SQL_ATTR_PARAMS_PROCESSED_PTR  
  
     SQL_ATTR_PARAMSET_SIZE  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_ROW_ARRAY_SIZE  
  
-   El uso de **SQLGetStmtAttr** para obtener los siguientes atributos de instrucción. (El uso de **SQLGetStmtAttr** para obtener otros atributos de instrucción es funcionalidad duplicada, no nueva funcionalidad.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Uso del tipo de datos de intervalo C, los tipos de datos SQL de intervalo, los tipos de datos BIGINT C y la estructura de datos SQL_C_NUMERIC.  
  
-   Enlace de parámetros en cuanto a fila.  
  
-   Capturas de marcadores basadas en desplazamiento, como llamar a **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_BOOKMARK y especificar un desplazamiento distinto de 0.  
  
-   **SQLFetch** devuelve la matriz de estado de fila, el número de filas recuperadas, la obtención de varias filas, la mezcla de llamadas con **SQLFetchScroll**y la mezcla de llamadas con **SQLBulkOperations** o **SQLSetPos**. Para obtener más información, vea la sección siguiente, Cursores de [bloque, Cursores desplazables y Compatibilidad con versiones anteriores para aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parámetros con nombre.  
  
-   Cualquiera de las opciones **SQLGetInfo** específicas de ODBC *3.x.* (Si una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* llama a los tipos de información SQL_XXX_CURSOR_ATTRIBUTES1, que han reemplazado varios tipos de información ODBC *2.x,* parte de la información podría ser confiable, pero algunos podrían ser poco confiables. Para obtener más información, vea [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Desplazamientos de enlace.  
  
-   Actualización, actualización y eliminación por marcadores (mediante una llamada a **SQLBulkOperations**).  
  
-   Llamar a **SQLBulkOperations** o **SQLSetPos** en el estado S5.  
  
-   Los campos ROW_NUMBER y COLUMN_NUMBER del registro de diagnóstico (que deben recuperarse las funciones de reemplazo **SQLGetDiagField** o **SQLGetDiagRec**).  
  
-   Recuentos aproximados de filas.  
  
-   Información de advertencia (SQL_ROW_SUCCESS_WITH_INFO desde **SQLFetchScroll**).  
  
-   Marcadores de longitud variable.  
  
-   Información de error ampliada para matrices de parámetros.  
  
-   Todas las nuevas columnas de los conjuntos de resultados devueltos por las funciones de catálogo.  
  
-   Uso de **SQLDescribeCol** y **SQLColAttribute** en la columna 0.  
  
-   Uso de cualquier atributo de columna específico de ODBC *3.x*en una llamada a **SQLColAttribute**.  
  
-   Uso de varios identificadores de entorno.  
  
 Esta sección contiene el tema siguiente.  
  
-   [Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
