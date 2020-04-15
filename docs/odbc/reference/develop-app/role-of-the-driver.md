---
title: Papel del conductor ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304289"
---
# <a name="role-of-the-driver"></a>Rol del controlador
El controlador comprueba todos los errores y advertencias no comprobados por el Administrador de controladores y ordena los registros de estado que genera. (Un ODBC 2. *x* controlador no ordena registros de estado.) Esto incluye errores y advertencias en el truncamiento de datos, la conversión de datos, la sintaxis y algunas transiciones de estado. El controlador también puede comprobar errores y advertencias parcialmente comprobados por el Administrador de controladores. Por ejemplo, aunque el Administrador de controladores comprueba si el valor de *Operation* en **SQLSetPos** es legal, el controlador debe comprobar si es compatible.  
  
 El controlador también asigna *errores nativos* , es decir, errores devueltos por el origen de datos, a SQLSTATEs. Por ejemplo, el controlador podría asignar una serie de errores nativos diferentes para la sintaxis SQL ilegal a SQLSTATE 42000 (error de sintaxis o infracción de acceso). El controlador devuelve el número de error nativo en el campo SQL_DIAG_NATIVE del registro de estado. La documentación del controlador debe mostrar cómo se asignan errores y advertencias desde el origen de datos a argumentos en **SQLGetDiagRec** y **SQLGetDiagField**.
