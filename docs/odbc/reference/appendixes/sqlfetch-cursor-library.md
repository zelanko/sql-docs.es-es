---
title: SQLFetch (biblioteca de cursores) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05bfa99a97afa812928e91b7f0a77ced1eb4d1eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLFetch** función en la biblioteca de cursores. Para obtener información general sobre **SQLFetch**, consulte [SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetch** no se pueden mezclar con llamadas a **SQLFetchScroll** o **SQLExtendedFetch**.  
  
 Si **SQLFetch** se llama con SQL_ATTR_ROW_ARRAY_SIZE establecido en un valor mayor que 1, la biblioteca de cursores pasará a la llamada al controlador. Si el controlador es una API ODBC 2. *x* controlador, se pasará por alto el tamaño del conjunto de filas y la llamada a **SQLFetch** devolverá una sola fila de datos.  
  
 Si se utiliza la biblioteca de cursores con una API ODBC 2. *x* controlador, un enlace de desplazamiento (como se define por el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR) no se usa cuando **SQLFetch** se llama.  
  
 Cuando se carga la biblioteca de cursores, no puede llamar una aplicación **SQLFetch** para capturar columnas de marcadores. La biblioteca de cursores pasa la llamada a **SQLFetch** mediante el controlador, pero la función para habilitar los marcadores y enlazar la columna de marcador intercepta las llamadas por la biblioteca de cursores.
