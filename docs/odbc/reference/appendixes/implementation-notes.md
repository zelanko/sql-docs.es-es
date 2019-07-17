---
title: Notas de implementación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95b60ba35a867135cfc1f823e08b1a99f0262ca9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135741"
---
# <a name="implementation-notes"></a>Notas de implementación
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 En esta sección se describe cómo se implementa la biblioteca de cursores ODBC. Describe cómo la biblioteca de cursores mantiene su memoria caché, ejecuta las instrucciones SQL e implementa funciones ODBC.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Caché de la biblioteca de cursores](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Procesamiento de instrucciones SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funciones ODBC y biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
