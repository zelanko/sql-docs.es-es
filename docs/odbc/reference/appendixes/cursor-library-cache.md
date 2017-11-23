---
title: "Caché de la biblioteca de cursores | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9346fd75ac9dcb857f0c8b4cd67eb30471ccebd4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="cursor-library-cache"></a>Caché de la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Para cada fila de datos del conjunto de resultados, la biblioteca de cursores almacena temporalmente los datos para cada columna enlazada, la longitud de los datos de cada columna enlazada y el estado de la fila. La biblioteca de cursores utiliza los valores de la caché para volver a través **SQLFetch** y **SQLFetchScroll** y para construir instrucciones buscadas para operaciones por posición. Para obtener más información, consulte [construir instrucciones buscar](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos de columna](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Longitud de datos de columna](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Estado de fila](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Ubicación de caché](../../../odbc/reference/appendixes/location-of-cache.md)
