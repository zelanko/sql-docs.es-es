---
title: SQLBindCol (Biblioteca de cursores) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305476"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLBindCol** en la biblioteca de cursores. Para obtener información general acerca de **SQLBindCol**, vea [SqlBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Una aplicación asigna uno o varios búferes para que la biblioteca de cursores devuelva el conjunto de filas actual. Llama a **SQLBindCol** una o más veces para enlazar estos búferes al conjunto de resultados.  
  
 Una aplicación puede llamar a **SQLBindCol** para volver a enlazar columnas de conjunto de resultados después de que haya denominado **SQLExtendedFetch**, **SQLFetch**o **SQLFetchScroll**, siempre que el tipo de datos C, el tamaño de columna y los dígitos decimales de la columna enlazada sigan siendo los mismos. La aplicación no necesita cerrar el cursor para volver a enlazar columnas a diferentes direcciones.  
  
 La biblioteca de cursores admite la configuración del atributo SQL_ATTR_ROW_BIND_OFFSET_PTR instrucción para utilizar desplazamientos de enlace. (**SQLBindCol** no tiene que ser llamado para que se produzca este reenlace.) Si la biblioteca de cursores se utiliza con un controlador ODBC *3.x,* el desplazamiento de enlace no se utiliza cuando **SQLFetch** se llama. El desplazamiento de enlace se utiliza si **sqlFetch** se llama cuando se utiliza la biblioteca de cursores con un controlador ODBC *2.x* porque **SQLFetch,** a continuación, se asigna a **SQLExtendedFetch**.  
  
 La biblioteca de cursores admite la llamada a **SQLBindCol** para enlazar la columna de marcador.  
  
 Cuando se trabaja con un controlador ODBC *2.x,* la biblioteca de cursores devuelve SQLSTATE HY090 (cadena no válida o longitud de búfer) cuando **sqlBindCol** se llama para establecer la longitud del búfer para una columna de marcador en un valor no igual a 4. Cuando se trabaja con un controlador ODBC *3.x,* la biblioteca de cursores permite que el búfer tenga cualquier tamaño.
