---
title: Comprobando la compatibilidad de las características y la variabilidad | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21495e538a554a477336d1a92926c11fe762c5af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062662"
---
# <a name="checking-feature-support-and-variability"></a>Comprobación de compatibilidad con las características y la variabilidad
Para comprobar la compatibilidad y la variabilidad de las características, las aplicaciones generalmente llaman a **SQLGetInfo**, **SQLGetFunctions**y **SQLGetTypeInfo**. Un buen punto de partida son los niveles de cumplimiento de la gramática de SQL y la API del controlador. Estos describen los niveles amplios de compatibilidad con las características. A continuación, la aplicación puede llamar a **SQLGetInfo** con otras opciones para determinar la compatibilidad o la variabilidad de las características que necesita, **SQLGetFunctions** para determinar si se admiten las funciones que necesita más allá del nivel de conformidad devuelto y **SQLGetTypeInfo** para determinar qué tipos de datos de SQL se admiten.  
  
 Una aplicación puede determinar si se admite una instrucción o un atributo de conexión mediante una llamada a **SQLSetStmtAttr** o **SQLSetConnectAttr** con ese atributo. Si la función devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, se admite el atributo; Si devuelve SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada), no se admite el atributo.  
  
 Las aplicaciones también pueden determinar una cantidad limitada de información antes de conectarse al controlador mediante una llamada a **SQLDrivers**.
