---
title: SQLBindCol (biblioteca de cursores) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a877b6cade18e59f12abfe807d8efa04363b3dcb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLBindCol** función en la biblioteca de cursores. Para obtener información general sobre **SQLBindCol**, consulte [SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Una aplicación asigna uno o varios búferes para devolver el conjunto de filas actual en la biblioteca de cursores. Llama **SQLBindCol** una o varias veces para enlazar estos búferes para el conjunto de resultados.  
  
 Una aplicación puede llamar a **SQLBindCol** volver a enlazar el resultado de establece las columnas después de haber llamado **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**, siempre y cuando el tipo de datos de C, tamaño de la columna y dígitos decimales de la columna dependiente que siguen siendo los mismos. La aplicación no necesita cerrar el cursor para volver a enlazar las columnas en las diferentes direcciones.  
  
 La biblioteca de cursores es compatible con el establecimiento del atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR usar desplazamientos de enlace. (**SQLBindCol** no tiene que llamar para este reenlace para que se produzca.) Si se utiliza la biblioteca de cursores con una aplicación ODBC 3 *.x* controlador, el ajuste de enlace no está utilizan una vez **SQLFetch** se llama. El desplazamiento de enlace se utiliza si **SQLFetch** se llama cuando se utiliza la biblioteca de cursores con una API ODBC 2. *x* controlador porque **SQLFetch** , a continuación, se asigna a **SQLExtendedFetch**.  
  
 La biblioteca de cursores admite las llamadas a **SQLBindCol** para enlazar la columna de marcador.  
  
 Cuando se trabaja con una API ODBC 2. *x* controlador, la biblioteca de cursores devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) al **SQLBindCol** se llama para establecer la longitud del búfer para una columna de marcador a un valor no es igual a 4. Cuando se trabaja con una aplicación ODBC 3 *.x* controlador, la biblioteca de cursores permite que el búfer de cualquier tamaño.
