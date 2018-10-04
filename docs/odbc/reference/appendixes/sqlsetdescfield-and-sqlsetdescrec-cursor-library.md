---
title: SQLSetDescField y SQLSetDescRec (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b390df48e676290696ae8080c8f671fd0e37bad8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727723"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField y SQLSetDescRec (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLSetDescField** y **SQLSetDescRec** funciones en la biblioteca de cursores. Para obtener información general acerca de estas funciones, vea [función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) y [función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 La biblioteca de cursores ejecuta **SQLSetDescField** cuando se llama para devolver el valor de los campos de conjunto de columnas de marcadores:  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 La biblioteca de cursores ejecuta las llamadas a **SQLSetDescRec** para una columna de marcador.  
  
 Cuando se trabaja con un ODBC 2. *x* controlador, la biblioteca de cursores devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) cuando **SQLSetDescField** o **SQLSetDescRec** se llama para establecer el SQL_DESC_OCTET_ Campo de longitud para el registro de marcador de un descartar a un valor no es igual a 4. Cuando se trabaja con una aplicación ODBC 3 *.x* controlador, la biblioteca de cursores permite que el búfer de cualquier tamaño.  
  
 La biblioteca de cursores ejecuta **SQLSetDescField** cuando se llama para devolver el valor del campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE o SQL_DESC_ROW_STATUS_PTR. Estos campos se pueden devolver para cualquier fila, no solo la fila del marcador.  
  
 La biblioteca de cursores no se ejecuta **SQLSetDescField** para cambiar cualquier campo de descriptor que no sea de los campos mencionados anteriormente. Si una aplicación llama a **SQLSetDescField** para establecer cualquier otro campo mientras se carga la biblioteca de cursores, la llamada se pasa al controlador.  
  
 La biblioteca de cursores admite el cambio de forma dinámica los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR de cualquier fila de un descriptor de fila de la aplicación (después de llamar a **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**). El campo SQL_DESC_OCTET_LENGTH_PTR puede cambiarse a un puntero nulo solo a desenlazar el búfer de longitud para una columna.  
  
 La biblioteca de cursores no se admite cambiar el campo SQL_DESC_BIND_TYPE en APD o descartar cuando se abre un cursor. El campo SQL_DESC_BIND_TYPE puede cambiarse después de que se cierra el cursor y antes de que se abre un nuevo cursor. Los únicos campos de descriptor que la biblioteca de cursores admite el cambio cuando se abre un cursor son SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_ROWS_PROCESSED_ PTR.  
  
 La biblioteca de cursores no permite modificar el campo SQL_DESC_COUNT de la descartar después **SQLExtendedFetch** o **SQLFetchScroll** se ha llamado y antes de que se ha cerrado el cursor.
