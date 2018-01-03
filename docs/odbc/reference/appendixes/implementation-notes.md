---
title: "Notas de implementación | Documentos de Microsoft"
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
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 017c58b72d1b190d8d11f08cf7ecce5ff58f65b1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="implementation-notes"></a>Notas de implementación
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Esta sección describe cómo se implementa la biblioteca de cursores ODBC. Describe cómo la biblioteca de cursores mantiene su memoria caché, ejecuta las instrucciones SQL e implementa funciones ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Caché de la biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Procesamiento de instrucciones SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funciones ODBC y biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
