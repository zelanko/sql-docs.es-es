---
title: SQLGetDescField y SQLGetDescRec (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 853a364b61b63d58da93111c75db0d7d723ee49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073915"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField y SQLGetDescRec (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLGetDescField** y **SQLGetDescRec** funciones en la biblioteca de cursores. Para obtener información general acerca de estas funciones, vea [función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) y [función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 La biblioteca de cursores ejecuta **SQLGetDescRec** para devolver los metadatos de columnas de marcadores. La biblioteca de cursores ejecuta **SQLGetDescField** para devolver los mismos campos devueltos por **SQLGetDescRec**, que son SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_ LONGITUD, SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_NULLABLE. Para mantener la coherencia, **SQLGetDescField** también devuelve SQL_DESC_UNNAMED.  
  
 La biblioteca de cursores ejecuta **SQLGetDescField** cuando se llama para devolver el valor de los siguientes campos que se establecen para columnas de marcadores de enlace: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_LENGTH.  
  
 La biblioteca de cursores ejecuta **SQLGetDescField** cuando se llama para devolver el valor del campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE o SQL_DESC_ROW_STATUS_PTR. Estos campos se pueden devolver para cualquier fila, no solo la fila del marcador.  
  
 Si una aplicación llama a **SQLGetDescField** para devolver el valor de cualquier campo que no se ha mencionado anteriormente, la biblioteca de cursores pasa la llamada al controlador.
