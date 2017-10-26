---
title: "Comprobación de compatibilidad con las características y la variabilidad | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5528f451adf12d12fe5cdb1c51f5c5d0053c9145
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="checking-feature-support-and-variability"></a>Comprobación de compatibilidad con las características y la variabilidad
Para comprobar la compatibilidad con las características y la variabilidad, las aplicaciones habitual es llamar a **SQLGetInfo**, **SQLGetFunctions**, y **SQLGetTypeInfo**. Un buen punto de partida es niveles de compatibilidad de gramática SQL y API del controlador. Se describen los amplios niveles de compatibilidad de características. A continuación, puede llamar la aplicación **SQLGetInfo** con otras opciones para determinar el soporte técnico o la variabilidad de las características que necesita, **SQLGetFunctions** para determinar si las funciones necesita más allá el valor devuelto se admite el nivel de conformidad, y **SQLGetTypeInfo** para determinar qué tipos de datos SQL son compatibles.  
  
 Una aplicación puede determinar si un atributo de instrucción o la conexión se admite mediante una llamada a **SQLSetStmtAttr** o **SQLSetConnectAttr** con ese atributo. Si la función devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, se admite el atributo; Si devuelve SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada), el atributo no es compatible.  
  
 Las aplicaciones también pueden determinar una cantidad limitada de información antes de conectarse al controlador mediante una llamada a **SQLDrivers**.

