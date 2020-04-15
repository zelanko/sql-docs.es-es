---
title: SQLFetch (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bee83ccb5497888b57a45673599af6b92931a704
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298725"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLFetch** en la biblioteca de cursores. Para obtener información general acerca de **SQLFetch**, vea [Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetch** no se pueden mezclar con llamadas a **SQLFetchScroll** o **SQLExtendedFetch**.  
  
 Si **SQLFetch** se llama con SQL_ATTR_ROW_ARRAY_SIZE establecido en un valor mayor que 1, la biblioteca de cursores pasará la llamada al controlador. Si el controlador es un ODBC 2. *x* controlador, el tamaño del conjunto de filas se omitirá y la llamada a **SQLFetch** devolverá una sola fila de datos.  
  
 Si la biblioteca de cursores se utiliza con un ODBC 2. *x* controlador, un desplazamiento de enlace (según lo definido por el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR) no se utiliza cuando **SQLFetch** se llama.  
  
 Cuando se carga la biblioteca de cursores, una aplicación no puede llamar a **SQLFetch** para capturar columnas de marcadores. La biblioteca de cursores pasa la llamada a **SQLFetch** al controlador, pero la biblioteca de cursores intercepta las llamadas de función para habilitar los marcadores y enlazar la columna de marcadores.
