---
title: Comprobación de compatibilidad de las características y la variabilidad | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b9af2cfd73556baca4870428cdcdfcee3e07191d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63217609"
---
# <a name="checking-feature-support-and-variability"></a>Comprobación de compatibilidad con las características y la variabilidad
Para comprobar la compatibilidad con las características y la variabilidad, las aplicaciones llaman a generalmente **SQLGetInfo**, **SQLGetFunctions**, y **SQLGetTypeInfo**. Un buen punto de partida es niveles de compatibilidad de gramática SQL y de API del controlador. Estos describen amplia niveles de compatibilidad de características. A continuación, puede llamar la aplicación **SQLGetInfo** con otras opciones para determinar el soporte técnico o la variabilidad de las características que necesita, **SQLGetFunctions** para determinar si las funciones necesita más allá de los datos devueltos se admiten el nivel de cumplimiento, y **SQLGetTypeInfo** para determinar qué tipos de datos SQL son compatibles.  
  
 Una aplicación puede determinar si un atributo de instrucción o la conexión es compatible con una llamada a **SQLSetStmtAttr** o **SQLSetConnectAttr** con ese atributo. Si la función devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, se admite el atributo; Si devuelve SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada), no se admite el atributo.  
  
 Las aplicaciones también pueden determinar una cantidad limitada de información antes de conectarse al controlador mediante una llamada a **SQLDrivers**.
