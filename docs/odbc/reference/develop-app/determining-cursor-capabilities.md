---
title: Determinar las capacidades del Cursor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 716471786400c030febb62ebf41c8422770a8c09
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47598374"
---
# <a name="determining-cursor-capabilities"></a>Determinar las capacidades del Cursor
Las cuatro opciones siguientes en **SQLGetInfo** describen qué tipos de cursores se admiten y cuáles son sus funciones:  
  
-   SQL_CURSOR_SENSITIVITY. Indica si un cursor es sensible a los cambios realizados por otro cursor.  
  
-   SQL_SCROLL_OPTIONS. Enumera los tipos de cursor compatibles (solo avance, estáticos, controlado por, dinámicos o mixtos). Todos los orígenes de datos deben admitir cursores de solo avance.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (según el tipo del cursor). Enumera los tipos de fetch admitidos por cursores desplazables. Los bits del valor devuelto corresponden a los tipos de captura en **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (según el tipo del cursor). Indica si pueden detectar los cursores estáticos y controlados por sus propias actualizaciones, eliminaciones e inserciones.  
  
 Una aplicación puede determinar las capacidades del cursor en tiempo de ejecución mediante una llamada a **SQLGetInfo** con estas opciones. Normalmente, esto se hace por aplicaciones genéricas. Las capacidades del cursor también se pueden determinar durante el desarrollo de aplicaciones y su uso codificado de forma rígida en la aplicación. Esto normalmente se realiza mediante aplicaciones verticales y personalizadas, pero también puede realizarse por aplicaciones genéricas que utiliza una implementación de cursor de cliente, como la biblioteca de cursores ODBC.
