---
title: Recuperando marcadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300075"
---
# <a name="retrieving-bookmarks"></a>Recuperar marcadores
Si la aplicación va a utilizar marcadores, debe establecer el atributo SQL_ATTR_USE_BOOKMARKS instrucción en SQL_UB_VARIABLE antes de preparar o ejecutar la instrucción. Esto es necesario porque la creación y el mantenimiento de marcadores pueden ser una operación costosa, por lo que los marcadores solo deben habilitarse cuando una aplicación puede hacer un uso adecuado de ellos.  
  
 Los marcadores se devuelven como columna 0 del conjunto de resultados. Hay tres formas en que una aplicación puede recuperarlas:  
  
-   Enlazar columna 0 del conjunto de resultados. **SQLFetch** o **SQLFetchScroll** devuelve los marcadores de cada fila del conjunto de filas junto con los datos de otras columnas enlazadas.  
  
-   Llame a **SQLSetPos** para colocar en una fila del conjunto de filas y, a continuación, llame a **SQLGetData** para la columna 0. Si un controlador admite marcadores, siempre debe admitir la capacidad de llamar a **SQLGetData** para la columna 0, incluso si no permite que las aplicaciones llamen a **SQLGetData** para otras columnas antes de la última columna enlazada.  
  
-   Llame a **SQLBulkOperations** con el argumento *Operation* establecido en SQL_ADD y la columna 0 enlazada. El cursor inserta la fila y devuelve el marcador de la fila en el búfer enlazado.
