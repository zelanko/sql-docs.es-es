---
title: Comprobaciones de errores y advertencias del Administrador de controladores ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee8a0f5ebfac8b6f87281806f07989f4980eb9b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305790"
---
# <a name="driver-manager-error-and-warning-checks"></a>Error del Administrador de controladores y las comprobaciones de advertencia
El Administrador de controladores implementa total o parcialmente una serie de funciones y, por lo tanto, comprueba todos o algunos de los errores y advertencias en esas funciones.  
  
-   El Administrador de controladores implementa **SQLDataSources** y **SQLDrivers** y comprueba todos los errores y advertencias en estas funciones.  
  
-   El Administrador de controladores comprueba si un controlador implementa **SQLGetFunctions**. Si el controlador no implementa **SQLGetFunctions**, el Administrador de controladores implementa y comprueba todos los errores y advertencias en él.  
  
-   El Administrador de controladores implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **SQLFreeHandle**, **SQLGetDiagRec**y **SQLGetDiagField** y comprueba si hay algunos errores en estas funciones. Puede devolver los mismos errores que el controlador para algunas de estas funciones porque ambas realizan operaciones similares. Por ejemplo, el Administrador de controladores o el controlador pueden devolver SQLSTATE IM008 (Error de diálogo) si uno no puede mostrar un cuadro de diálogo de inicio de sesión para **SQLDriverConnect**.
