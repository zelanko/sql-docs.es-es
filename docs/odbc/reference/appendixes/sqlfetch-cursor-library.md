---
title: SQLFetch (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 487a6b357d21ee675fa9594d32c7a2bb7c66e400
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199493"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLFetch** función en la biblioteca de cursores. Para obtener información general sobre **SQLFetch**, consulte [función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Cuando se utiliza la biblioteca de cursores, las llamadas a **SQLFetch** no se pueden mezclar con las llamadas a **SQLFetchScroll** o **SQLExtendedFetch**.  
  
 Si **SQLFetch** se llama con SQL_ATTR_ROW_ARRAY_SIZE establecido en un valor mayor que 1, la biblioteca de cursores pasará a la llamada al controlador. Si el controlador es un ODBC 2. *x* controlador, se omitirá el tamaño del conjunto de filas y la llamada a **SQLFetch** devolverá una sola fila de datos.  
  
 Si se usa la biblioteca de cursores con un ODBC 2. *x* controlador, un enlace de desplazamiento (como se define por el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR) no es cuando usa **SQLFetch** se llama.  
  
 Cuando se carga la biblioteca de cursores, no puede llamar una aplicación **SQLFetch** para capturar las columnas de marcadores. La biblioteca de cursores pasa la llamada a **SQLFetch** a través para el controlador, pero la función se interceptan las llamadas a habilitar marcadores y enlazar la columna de marcador por la biblioteca de cursores.
