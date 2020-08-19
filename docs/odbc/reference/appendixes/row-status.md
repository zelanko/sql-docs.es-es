---
description: Estado de fila
title: Estado de fila | Microsoft Docs
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
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8970e78d523ca86a50edb1e27b159ef15a1a1747
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424967"
---
# <a name="row-status"></a>Estado de fila
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 La biblioteca de cursores crea un búfer en la memoria caché para el estado de la fila. La biblioteca de cursores recupera los valores de la matriz de estado de fila (especificada con el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR) de este búfer. Para cada fila, la biblioteca de cursores establece este búfer en:  
  
-   SQL_ROW_DELETED cuando ejecuta una instrucción Delete posicionada en la fila.  
  
-   SQL_ROW_ERROR cuando encuentra un error al recuperar la fila del origen de datos con **SQLFetch**.  
  
-   SQL_ROW_SUCCESS cuando captura correctamente la fila del origen de datos con **SQLFetch**.  
  
-   SQL_ROW_UPDATED cuando ejecuta una instrucción UPDATE posicionada en la fila.
