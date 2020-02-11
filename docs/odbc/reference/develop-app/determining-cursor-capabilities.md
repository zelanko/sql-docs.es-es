---
title: Determinar las capacidades del cursor | Microsoft Docs
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
ms.openlocfilehash: 14715e40cd99f3f1a03c2ae19e825705a8376e30
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039999"
---
# <a name="determining-cursor-capabilities"></a>Determinar las capacidades del Cursor
Las cuatro opciones siguientes de **SQLGetInfo** describen qué tipos de cursores se admiten y cuáles son sus capacidades:  
  
-   SQL_CURSOR_SENSITIVITY. Indica si un cursor es sensible a los cambios realizados por otro cursor.  
  
-   SQL_SCROLL_OPTIONS. Enumera los tipos de cursor admitidos (solo avance, estático, controlado por conjunto de claves, dinámico o mixto). Todos los orígenes de datos deben admitir cursores de solo avance.  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (dependiendo del tipo de cursor). Enumera los tipos de captura que admiten los cursores desplazables. Los bits del valor devuelto corresponden a los tipos de captura en **SQLFetchScroll**.  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 o SQL_STATIC_CURSOR_ATTRIBUTES2 (dependiendo del tipo de cursor). Muestra si los cursores estáticos y los controlados por conjunto de claves pueden detectar sus propias actualizaciones, eliminaciones e inserciones.  
  
 Una aplicación puede determinar las capacidades del cursor en tiempo de ejecución mediante una llamada a **SQLGetInfo** con estas opciones. Esto lo suelen hacer las aplicaciones genéricas. También se pueden determinar las capacidades de cursor durante el desarrollo de la aplicación y su uso codificado de forma rígida en la aplicación. Esto se realiza normalmente mediante aplicaciones verticales y personalizadas, pero también se puede hacer mediante aplicaciones genéricas que usan una implementación de cursor del lado cliente, como la biblioteca de cursores ODBC.
