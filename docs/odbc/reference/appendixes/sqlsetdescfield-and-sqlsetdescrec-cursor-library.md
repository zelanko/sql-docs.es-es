---
title: SQLSetDescField y SQLSetDescRec (biblioteca de cursores) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04c3fd1c3c64140b7669cdeeb35937498249ac66
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910280"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField y SQLSetDescRec (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLSetDescField** y **SQLSetDescRec** funciones en la biblioteca de cursores. Para obtener información general acerca de estas funciones, vea [sqlsetdescfield, función](../../../odbc/reference/syntax/sqlsetdescfield-function.md) y [sqlsetdescrec, función](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
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
  
 La biblioteca de cursores ejecuta llamadas a **SQLSetDescRec** para una columna de marcador.  
  
 Cuando se trabaja con una API ODBC 2. *x* controlador, la biblioteca de cursores devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) al **SQLSetDescField** o **SQLSetDescRec** se llama para establecer el SQL_DESC_OCTET_ Campo de longitud para el registro de marcador de un descartar en un valor no es igual a 4. Cuando se trabaja con una aplicación ODBC 3 *.x* controlador, la biblioteca de cursores permite que el búfer de cualquier tamaño.  
  
 La biblioteca de cursores ejecuta **SQLSetDescField** cuando se llama para devolver el valor del campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE o SQL_DESC_ROW_STATUS_PTR. Estos campos se pueden devolver las filas, no solo la fila de marcador.  
  
 La biblioteca de cursores no se ejecuta **SQLSetDescField** para cambiar cualquier campo de descriptor que no sean los campos que se ha mencionado anteriormente. Si una aplicación llama **SQLSetDescField** para establecer cualquier otro campo mientras se carga la biblioteca de cursores, la llamada se transfiere a través del controlador.  
  
 La biblioteca de cursores admite el cambio de forma dinámica los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR de cualquier fila de un descriptor de fila de la aplicación (después de llamar a **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**). El campo SQL_DESC_OCTET_LENGTH_PTR puede cambiarse a un puntero nulo solo a desenlazar el búfer de longitud de una columna.  
  
 La biblioteca de cursores no admite el cambio del campo SQL_DESC_BIND_TYPE en un APD o descartar cuando se abre un cursor. El campo SQL_DESC_BIND_TYPE puede cambiarse después de que se cierra el cursor y antes de que se abre un nuevo cursor. Los únicos campos de descriptor que la biblioteca de cursores admite el cambio cuando se abre un cursor son SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_ROWS_PROCESSED_ PTR.  
  
 La biblioteca de cursores no permite modificar el campo SQL_DESC_COUNT de la descartar después **SQLExtendedFetch** o **SQLFetchScroll** se ha llamado y antes de que se ha cerrado el cursor.
