---
title: Comprobaciones de errores y advertencias del administrador de controladores | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305790"
---
# <a name="driver-manager-error-and-warning-checks"></a>Error del Administrador de controladores y las comprobaciones de advertencia
El administrador de controladores implementa de forma completa o parcial varias funciones y, por lo tanto, comprueba todos los errores y advertencias de esas funciones, o algunos de ellos.  
  
-   El administrador de controladores implementa **SQLDataSources** y **SQLDrivers** y comprueba todos los errores y advertencias de estas funciones.  
  
-   El administrador de controladores comprueba si un controlador implementa **SQLGetFunctions**. Si el controlador no implementa **SQLGetFunctions**, el administrador de controladores implementa y comprueba si hay errores y advertencias en él.  
  
-   El administrador de controladores implementa parcialmente **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, **SQLFreeHandle**, **SQLGetDiagRec**y **SQLGetDiagField** y comprueba algunos errores en estas funciones. Puede devolver los mismos errores que el controlador de algunas de estas funciones porque realizan operaciones similares. Por ejemplo, el administrador de controladores o el controlador pueden devolver SQLSTATE IM008 (error de cuadro de diálogo) si cualquiera de los dos no puede mostrar un cuadro de diálogo de inicio de sesión para **SQLDriverConnect**.
