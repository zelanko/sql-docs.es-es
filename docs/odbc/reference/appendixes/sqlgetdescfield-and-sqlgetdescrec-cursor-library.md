---
title: SQLGetDescField y SQLGetDescRec (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ceea6b6180e1b51f2f103f74412c3e2b4cbe02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307836"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField y SQLGetDescRec (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de las **funciones SQLGetDescField** y **SQLGetDescRec** en la biblioteca de cursores. Para obtener información general sobre estas funciones, vea [SQLGetDescField (Función)](../../../odbc/reference/syntax/sqlgetdescfield-function.md) y [SQLGetDescRec (Función).](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
 La biblioteca de cursores ejecuta **SQLGetDescRec** para devolver metadatos para las columnas de marcador. La biblioteca de cursores ejecuta **SQLGetDescField** para devolver los mismos campos devueltos por **SQLGetDescRec**, que son SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_NULLABLE. Por coherencia, **SQLGetDescField** también devuelve SQL_DESC_UNNAMED.  
  
 La biblioteca de cursores ejecuta **SQLGetDescField** cuando se llama para devolver el valor de los siguientes campos que se establecen para enlazar columnas de marcadores: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_LENGTH.  
  
 La biblioteca de cursores ejecuta **SQLGetDescField** cuando se llama para devolver el valor del campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE o SQL_DESC_ROW_STATUS_PTR. Estos campos se pueden devolver para cualquier fila, no solo para la fila de marcadores.  
  
 Si una aplicación llama a **SQLGetDescField** para devolver el valor de cualquier campo distinto de los mencionados anteriormente, la biblioteca de cursores pasa la llamada al controlador.
