---
title: Nuevas características | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 74c9a97c2511bc9c9a738b9e63548a9179552489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086342"
---
# <a name="new-features"></a>Nuevas características
Se ha introducido la nueva funcionalidad siguiente en ODBC *3.x*. Un ODBC *3.x* la aplicación funciona con un ODBC *2.x* controlador no podrá utilizar esta funcionalidad. ODBC *3.x* Administrador de controladores no se asigna estas características cuando se trabaja con un ODBC *2.x* controlador.  
  
-   Las funciones que toman un descriptor de controlan como argumento: **SQLSetDescField**, **SQLGetDescField**, **SQLSetDescRec**, **SQLGetDescRec**, y **SQLCopyDesc**.  
  
-   Las funciones **SQLSetEnvAttr** y **SQLGetEnvAttr**.  
  
-   El uso de **SQLAllocHandle** para asignar un identificador de descriptor. (El uso de **SQLAllocHandle** asignar identificadores de entorno, la conexión y la instrucción está duplicado, no sobre las nuevas funciones.)  
  
-   El uso de **SQLGetConnectAttr** para obtener los atributos de conexión SQL_ATTR_AUTO_IPD. (El uso de **SQLSetConnectAttr** para establecer, y **SQLGetConnectAttr** para obtener, otros atributos de conexión está duplicado, no sobre las nuevas funciones.)  
  
-   El uso de **SQLSetStmtAttr** para establecer, y **SQLGetStmtAttr** para obtener los siguientes atributos de instrucción. (El uso de **SQLSetStmtAttr** para establecer, y **SQLGetStmtAttr** para obtener, otros atributos de instrucción es una funcionalidad duplicada, no es nueva.)  
  
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
  
-   El uso de **SQLGetStmtAttr** para obtener los siguientes atributos de instrucción. (El uso de **SQLGetStmtAttr** para obtener otra instrucción atributos es una funcionalidad duplicada, no la nueva funcionalidad.)  
  
     SQL_ATTR_IMP_ROW_DESC SQL_ATTR_IMP_PARAM_DESC  
  
-   Uso de los tipos de datos SQL de intervalo, el tipo de datos C de intervalo, los tipos de datos BIGINT C y la estructura de datos SQL_C_NUMERIC.  
  
-   El enlace de parámetros.  
  
-   Captura de marcador basados en el desplazamiento, como la llamada a **SQLFetchScroll** con un *FetchOrientation* argumento de SQL_FETCH_BOOKMARK y especificando un desplazamiento distinto de 0.  
  
-   **SQLFetch** devolver la matriz de Estados de fila, número de filas recuperado, capturar varias filas, llama a mezclar con **SQLFetchScroll**y llama a mezclar con **SQLBulkOperations** o **SQLSetPos**. Para obtener más información, consulte la sección siguiente, [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
-   Parámetros con nombre.  
  
-   Cualquiera de ODBC *3.x*-específico **SQLGetInfo** opciones. (Si un ODBC *3.x* la aplicación funciona con un ODBC *2.x* controlador llama a los tipos de información SQL_XXX_CURSOR_ATTRIBUTES1, que se han reemplazado ODBC varios *2.x* tipos de información, parte de la información podría ser confiable, pero algunos podrían no ser confiables. Para obtener más información, consulte [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).)  
  
-   Enlazar los desplazamientos.  
  
-   Actualizar, actualizar y eliminar mediante marcadores (mediante una llamada a **SQLBulkOperations**).  
  
-   Una llamada a **SQLBulkOperations** o **SQLSetPos** en el estado S5.  
  
-   Los campos ROW_NUMBER y núm_columna en el registro de diagnóstico (que tienen que recuperarse por las funciones de reemplazo **SQLGetDiagField** o **SQLGetDiagRec**).  
  
-   Recuentos de filas aproximado.  
  
-   Información de advertencia (SQL_ROW_SUCCESS_WITH_INFO desde **SQLFetchScroll**).  
  
-   Marcadores de longitud variable.  
  
-   Información de error extendida para las matrices de parámetros.  
  
-   Todas las columnas nuevas en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
-   El uso de **SQLDescribeCol** y **SQLColAttribute** en la columna 0.  
  
-   Uso de cualquier ODBC *3.x*-atributos de columna específica en una llamada a **SQLColAttribute**.  
  
-   Uso de varios identificadores de entorno.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Cursores de bloque y los cursores desplazables, compatibilidad con versiones anteriores de las aplicaciones ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)
