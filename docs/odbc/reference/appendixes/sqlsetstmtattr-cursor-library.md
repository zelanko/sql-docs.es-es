---
title: SQLSetStmtAttr (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC], Cursor Library
ms.assetid: 6018a733-c2c8-4047-92ec-92cf85031767
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bdd9b3b559d5cc78a0d44f5280aae347bc8996a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300495"
---
# <a name="sqlsetstmtattr-cursor-library"></a>SQLSetStmtAttr (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLSetStmtAttr** en la biblioteca de cursores. Para obtener información general acerca de **SQLSetStmtAttr**, vea [SQLSetStmtAttr (Función)](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
 La biblioteca de cursores admite los siguientes atributos de instrucción con **SQLSetStmtAttr:**  
  
|||  
|-|-|  
|SQL_ATTR_CONCURRENCY|SQL_ATTR_ROW_BIND_OFFSET_PTR|  
|SQL_ATTR_CURSOR_TYPE|SQL_ATTR_ROW_BIND_TYPE|  
|SQL_ATTR_FETCH_BOOKMARK_PTR|SQL_ATTR_ROWSET_ARRAY_SIZE|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_ATTR_SIMULATE_CURSOR|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_ATTR_USE_BOOKMARKS|  
  
 La biblioteca de cursores solo admite los valores SQL_CURSOR_FORWARD_ONLY y SQL_CURSOR_STATIC del atributo de instrucción SQL_ATTR_CURSOR_TYPE.  
  
 Para cursores de solo avance, la biblioteca de cursores admite el valor SQL_CONCUR_READ_ONLY del atributo de instrucción SQL_ATTR_CONCURRENCY. Para los cursores estáticos, la biblioteca de cursores admite los valores SQL_CONCUR_READ_ONLY y SQL_CONCUR_VALUES del atributo de instrucción SQL_ATTR_CONCURRENCY.  
  
 La biblioteca de cursores solo admite el valor SQL_SC_NON_UNIQUE del atributo de instrucción SQL_ATTR_SIMULATE_CURSOR.  
  
 Aunque la especificación ODBC admite llamadas a **SQLSetStmtAttr** con los atributos SQL_ATTR_PARAM_BIND_TYPE o SQL_ATTR_ROW_BIND_TYPE después de **sqlFetch** o **SQLFetchScroll** se ha llamado, la biblioteca de cursores no lo hace. Antes de que pueda cambiar el tipo de enlace en la biblioteca de cursores, la aplicación debe cerrar el cursor. La biblioteca de cursores admite el cambio de los atributos de SQL_ATTR_ROW_BIND_OFFSET_PTR, SQL_ATTR_PARAM_BIND_OFFSET_PTR, SQL_ATTR_ROWS_FETCHED_PTR y SQL_ATTR_PARAMS_PROCESSED_PTR instrucción cuando un cursor está abierto.  
  
 Una aplicación puede llamar a **SQLSetStmtAttr** con un **atributo** de SQL_ATTR_ROW_ARRAY_SIZE para cambiar el tamaño del conjunto de filas mientras está abierto un cursor. El nuevo tamaño del conjunto de filas surtirá efecto la próxima vez **que SQLFetchScroll** o **SQLFetch** se llama.  
  
 La biblioteca de cursores admite la configuración del atributo de instrucción SQL_ATTR_PARAM_BIND_OFFSET_PTR o SQL_ATTR_ROW_BIND_OFFSET_PTR para habilitar los desplazamientos de enlace. El desplazamiento de enlace no se usará para las llamadas a **SQLFetch** cuando se usa la biblioteca de cursores con un ODBC 2. *x* conductor.  
  
 La biblioteca de cursores admite la configuración del atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE.
