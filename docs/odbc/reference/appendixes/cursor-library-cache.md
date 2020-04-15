---
title: Caché de la biblioteca de cursores (En lo que se puede almacenar Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5686bf0c3e261b1df947c02e2edaa419da498ecb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284695"
---
# <a name="cursor-library-cache"></a>Caché de la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Para cada fila de datos del conjunto de resultados, la biblioteca de cursores almacena en caché los datos de cada columna enlazada, la longitud de los datos de cada columna enlazada y el estado de la fila. La biblioteca de cursores utiliza los valores de la memoria caché tanto para devolver a través de **SQLFetch** y **SQLFetchScroll** como para construir instrucciones buscadas para las operaciones posicionadas. Para obtener más información, vea [Construir instrucciones buscadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos de columna](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Longitud de datos de columna](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Estado de fila](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Ubicación de caché](../../../odbc/reference/appendixes/location-of-cache.md)
