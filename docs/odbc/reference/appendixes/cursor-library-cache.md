---
title: "Caché de la biblioteca de cursores | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
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
ms.openlocfilehash: 0da55a85fa5f8e1fd53656aa1cac37959a4200f7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
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
