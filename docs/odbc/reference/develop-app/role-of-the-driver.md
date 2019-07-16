---
title: Rol del controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c344c1d8b3a4702728807af9dae7ed9ca7c5cd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020384"
---
# <a name="role-of-the-driver"></a>Rol del controlador
El controlador comprueba todos los errores y advertencias no activadas por el Administrador de controladores y ordena los registros de estado que genera. (Un ODBC 2. *x* controlador no ordena los registros de estado.) Esto incluye errores y advertencias de truncamiento de datos, la conversión de datos, la sintaxis y algunas transiciones de estado. También puede comprobar el controlador de errores y advertencias activadas parcialmente por el Administrador de controladores. Por ejemplo, aunque el Administrador de controladores comprueba si el valor de *operación* en **SQLSetPos** es legal, el controlador debe comprobar si se admite.  
  
 El controlador también asigna *errores nativos* : es decir, los errores devueltos por el origen de datos - a SQLSTATEs. Por ejemplo, el controlador podría asignar un número de errores nativos diferentes para ilegal sintaxis SQL para SQLSTATE 42000 (sintaxis o infracción de acceso). El controlador devuelve el número de error nativo en el campo SQL_DIAG_NATIVE del registro de estado. Documentación del controlador debe mostrar cómo errores y advertencias se asignan desde el origen de datos para los argumentos de **SQLGetDiagRec** y **SQLGetDiagField**.
