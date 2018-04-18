---
title: Error del Administrador de controladores y las comprobaciones de advertencia | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f212af4169b4c0be2a840f6ff8d7310abb40f53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="driver-manager-error-and-warning-checks"></a>Error del Administrador de controladores y las comprobaciones de advertencia
El Administrador de controladores por completo o parcial implementa una serie de funciones y, por tanto, comprueba todos o algunos de los errores y advertencias en esas funciones.  
  
-   Implementa el Administrador de controladores **SQLDataSources** y **SQLDrivers** y comprueba si todos los errores y advertencias en estas funciones.  
  
-   El Administrador de controladores comprueba si implementa un controlador **SQLGetFunctions**. Si el controlador no implementa **SQLGetFunctions**, el Administrador de controladores se implementa y se comprueba si todos los errores y advertencias en ella.  
  
-   El Administrador de controladores parcialmente implementa **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, y **SQLGetDiagField** y comprueba si hay algunos errores en estas funciones. Pueden devolver los mismos errores como el controlador para algunas de estas funciones porque ambos realizan operaciones similares. Por ejemplo, el Administrador de controladores o el controlador puede devolver SQLSTATE IM008 (cuadro de diálogo no se pudo) si el valor es no se puede mostrar un cuadro de diálogo de inicio de sesión para una **SQLDriverConnect**.
