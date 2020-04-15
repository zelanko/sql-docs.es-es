---
title: Comprobación de la compatibilidad con funciones y variabilidad de la función de la función de la clase de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47f16160c05d1c410e3889f0bb857befe88df5b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299175"
---
# <a name="checking-feature-support-and-variability"></a>Comprobación de compatibilidad con las características y la variabilidad
Para comprobar la compatibilidad y la variabilidad de las características, las aplicaciones suelen llamar a **SQLGetInfo**, **SQLGetFunctions**y **SQLGetTypeInfo**. Un buen punto de partida es la API del controlador y los niveles de conformidad de la gramática SQL. Estos describen amplios niveles de compatibilidad con características. A continuación, la aplicación puede llamar a **SQLGetInfo** con otras opciones para determinar la compatibilidad o variabilidad de las características que necesita, **SQLGetFunctions** para determinar si se admiten las funciones que necesita más allá del nivel de conformidad devuelto y **SQLGetTypeInfo** para determinar qué tipos de datos SQL se admiten.  
  
 Una aplicación puede determinar si una instrucción o atributo de conexión se admite mediante una llamada a **SQLSetStmtAttr** o **SQLSetConnectAttr** con ese atributo. Si la función devuelve SQL_SUCCESS u SQL_SUCCESS_WITH_INFO, se admite el atributo; si devuelve SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada), no se admite el atributo.  
  
 Las aplicaciones también pueden determinar una cantidad limitada de información antes de conectarse al controlador llamando a **SQLDrivers**.
