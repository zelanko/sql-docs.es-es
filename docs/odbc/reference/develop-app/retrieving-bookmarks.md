---
title: Recuperar marcadores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d7d4bd52a5f6e5b03a084cef4402e0a9044f97d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861405"
---
# <a name="retrieving-bookmarks"></a>Recuperar marcadores
Si la aplicación va a usar marcadores, se debe establecer el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE antes de preparar o ejecutar la instrucción. Esto es necesario porque crear y mantener marcadores pueden ser una operación costosa, por lo que deben habilitarse marcadores solo cuando una aplicación puede hacer buen usan de los mismos.  
  
 Los marcadores se devuelven como columna 0 del conjunto de resultados. Hay tres formas de que una aplicación puede recuperarlos:  
  
-   Enlazar la columna 0 del conjunto de resultados. **SQLFetch** o **SQLFetchScroll** devuelve los marcadores para cada fila del conjunto de filas junto con los datos para otras columnas enlazadas.  
  
-   Llame a **SQLSetPos** para colocar una fila del conjunto de filas y, a continuación, llame a **SQLGetData** para la columna 0. Si un controlador es compatible con marcadores, siempre debe admitir la posibilidad de llamar a **SQLGetData** para la columna 0, incluso si no permite las aplicaciones llamen a **SQLGetData** para otras columnas antes de la última enlazados columna.  
  
-   Llame a **SQLBulkOperations** con el *operación* argumento establecido en SQL_ADD y enlaza la columna 0. El cursor inserta la fila y devuelve el marcador de la fila en el búfer enlazado.
