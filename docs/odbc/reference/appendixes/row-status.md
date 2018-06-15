---
title: Estado de fila | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba4f36ad63ee5e7d9fada29d444e8cc36eca1bcf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906310"
---
# <a name="row-status"></a>Estado de fila
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 La biblioteca de cursores, crea un búfer en la memoria caché para que el estado de fila. La biblioteca de cursores recupera valores de la matriz de Estados de fila (especificado con el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR) de este búfer. Para cada fila, la biblioteca de cursores establece este búfer en:  
  
-   SQL_ROW_DELETED cuando ejecuta una posición delete, instrucción en la fila.  
  
-   SQL_ROW_ERROR cuando encuentra un error al recuperar la fila del origen de datos con **SQLFetch**.  
  
-   SQL_ROW_SUCCESS cuando captura correctamente la fila del origen de datos con **SQLFetch**.  
  
-   SQL_ROW_UPDATED cuando ejecuta una instrucción de actualización por posición en la fila.
