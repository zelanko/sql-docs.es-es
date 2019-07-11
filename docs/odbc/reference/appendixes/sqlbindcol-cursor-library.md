---
title: SQLBindCol (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cd98b39421e95254fcb052db67cbc9f9205b668
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793532"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLBindCol** función en la biblioteca de cursores. Para obtener información general sobre **SQLBindCol**, consulte [función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Una aplicación asigna uno o varios búferes para la biblioteca de cursores devolver el conjunto de filas actual. Llama a **SQLBindCol** una o varias veces para enlazar estos búferes al conjunto de resultados.  
  
 Una aplicación puede llamar a **SQLBindCol** para volver a enlazar el resultado de establece las columnas después de haber llamado **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**, siempre que el tipo de datos C, tamaño de la columna y los dígitos decimales de la columna dependiente que siguen siendo los mismos. La aplicación no necesita cerrar el cursor para volver a enlazar columnas a diferentes direcciones.  
  
 La biblioteca de cursores es compatible con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR utilizar desplazamientos de enlace. (**SQLBindCol** no tiene que llamarse para este reenlace para que se produzca.) Si se utiliza la biblioteca de cursores con un ODBC *3.x* controlador, el desplazamiento de enlace no es cuando usa **SQLFetch** se llama. El desplazamiento de enlace se utiliza si **SQLFetch** se llama cuando se usa la biblioteca de cursores con un ODBC *2.x* controlador porque **SQLFetch** , a continuación, se asigna a  **SQLExtendedFetch**.  
  
 Admite las llamadas a la biblioteca de cursores **SQLBindCol** para enlazar la columna de marcador.  
  
 Cuando se trabaja con un ODBC *2.x* controlador, la biblioteca de cursores devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) cuando **SQLBindCol** se llama para establecer la longitud del búfer para una columna de marcador en un valor no igual a 4. Cuando se trabaja con un ODBC *3.x* controlador, la biblioteca de cursores permite que el búfer de cualquier tamaño.
