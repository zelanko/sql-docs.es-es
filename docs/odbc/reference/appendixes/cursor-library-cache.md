---
title: Caché de la biblioteca de cursores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597abe268979852d754e2e3e86ae81daa8f3fed8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019057"
---
# <a name="cursor-library-cache"></a>Caché de la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Para cada fila de datos del conjunto de resultados, la biblioteca de cursores almacena en caché los datos para cada columna enlazada, la longitud de los datos de cada columna enlazada y el estado de la fila. La biblioteca de cursores utiliza los valores de la caché para volver a través de **SQLFetch** y **SQLFetchScroll** y para construir instrucciones buscadas para operaciones por posición. Para obtener más información, consulte [construir busca instrucciones](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [Datos de columna](../../../odbc/reference/appendixes/column-data.md)  
  
-   [Longitud de datos de columna](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [Estado de fila](../../../odbc/reference/appendixes/row-status.md)  
  
-   [Ubicación de caché](../../../odbc/reference/appendixes/location-of-cache.md)
