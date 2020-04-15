---
title: Determinación de las capacidades del cursor ( Determining Cursor Capabilities) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 984ad8302f2e1695c8df84a64a18042f4cc9e364
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305886"
---
# <a name="determining-cursor-capabilities"></a>Determinar las capacidades del Cursor
Las cuatro opciones siguientes de **SQLGetInfo** describen qué tipos de cursores se admiten y cuáles son sus capacidades:  
  
-   SQL_CURSOR_SENSITIVITY. Indica si un cursor es sensible a los cambios realizados por otro cursor.  
  
-   SQL_SCROLL_OPTIONS. Enumera los tipos de cursor admitidos (solo hacia delante, estáticos, controlados por conjuntos de claves, dinámicos o mixtos). Todos los orígenes de datos deben admitir cursores de solo avance.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (dependiendo del tipo de cursor). Enumera los tipos de captura admitidos por los cursores desplazables. Los bits del valor devuelto corresponden a los tipos fetch de **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (dependiendo del tipo de cursor). Enumera si los cursores estáticos y controlados por conjuntos de claves pueden detectar sus propias actualizaciones, eliminaciones e inserciones.  
  
 Una aplicación puede determinar las capacidades del cursor en tiempo de ejecución mediante una llamada a **SQLGetInfo** con estas opciones. Esto se hace comúnmente por aplicaciones genéricas. Las capacidades del cursor también se pueden determinar durante el desarrollo de la aplicación y su uso codificado de forma rígida en la aplicación. Esto se hace normalmente por aplicaciones verticales y personalizadas, pero también lo pueden hacer las aplicaciones genéricas que usan una implementación de cursor del lado cliente, como la biblioteca de cursores ODBC.
