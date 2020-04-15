---
title: Recuperación de marcadores ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300075"
---
# <a name="retrieving-bookmarks"></a>Recuperar marcadores
Si la aplicación usará marcadores, debe establecer el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE antes de preparar o ejecutar la instrucción. Esto es necesario porque crear y mantener marcadores puede ser una operación costosa, por lo que los marcadores deben habilitarse solo cuando una aplicación puede hacer un buen uso de ellos.  
  
 Los marcadores se devuelven como columna 0 del conjunto de resultados. Hay tres maneras en que una aplicación puede recuperarlos:  
  
-   Enlazar la columna 0 del conjunto de resultados. **SQLFetch** o **SQLFetchScroll** devuelve los marcadores de cada fila del conjunto de filas junto con los datos de otras columnas enlazadas.  
  
-   Llame a **SQLSetPos** para colocar en una fila en el conjunto de filas y, a continuación, llame a **SQLGetData** para la columna 0. Si un controlador admite marcadores, siempre debe admitir la capacidad de llamar a **SQLGetData** para la columna 0, incluso si no permite que las aplicaciones llamen a **SQLGetData** para otras columnas antes de la última columna enlazada.  
  
-   Llame a **SQLBulkOperations** con el *Operación* argumento establecido en SQL_ADD y columna 0 enlazado. El cursor inserta la fila y devuelve el marcador de la fila en el búfer enlazado.
