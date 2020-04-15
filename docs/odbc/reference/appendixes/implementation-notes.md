---
title: Notas de implementación ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 970188a2fca45706405e398cece0f04d38dfdc68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284319"
---
# <a name="implementation-notes"></a>Notas de implementación
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En esta sección se describe cómo se implementa la biblioteca de cursores ODBC. Describe cómo la biblioteca de cursores mantiene su caché, ejecuta instrucciones SQL e implementa funciones ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Caché de la biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Procesamiento de instrucciones SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funciones ODBC y biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
