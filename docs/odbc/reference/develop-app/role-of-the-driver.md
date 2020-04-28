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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c683d990aaa3fd6892369e734c06fd1c356bd0f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304289"
---
# <a name="role-of-the-driver"></a>Rol del controlador
El controlador comprueba todos los errores y advertencias no comprobados por el administrador de controladores y los registros de estado de los pedidos que genera. (ODBC 2. el controlador *x* no ordena los registros de estado). Esto incluye errores y advertencias en el truncamiento de datos, la conversión de datos, la sintaxis y algunas transiciones de estado. El controlador también puede comprobar errores y advertencias que el administrador de controladores ha activado parcialmente. Por ejemplo, aunque el administrador de controladores comprueba si el valor de *Operation* en **SQLSetPos** es legal, el controlador debe comprobar si es compatible.  
  
 El controlador también asigna *errores nativos* , es decir, errores devueltos por el origen de datos a SQLSTATEs. Por ejemplo, el controlador podría asignar varios errores nativos diferentes para la sintaxis SQL no válida a SQLSTATE 42000 (error de sintaxis o infracción de acceso). El controlador devuelve el número de error nativo en el campo SQL_DIAG_NATIVE del registro de estado. La documentación del controlador debe mostrar cómo se asignan los errores y las advertencias desde el origen de datos a los argumentos de **SQLGetDiagRec** y **SQLGetDiagField**.
