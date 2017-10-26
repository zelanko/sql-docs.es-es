---
title: Rol del controlador | Documentos de Microsoft
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
- driver error checking [ODBC]
- diagnostic information [ODBC], driver error checking
ms.assetid: cac64c24-a27d-4884-96c0-ea7988351711
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2fe0d0545bcc787275bda3ba2154088f23eeda20
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="role-of-the-driver"></a>Rol del controlador
El controlador busca todos los errores y advertencias no activadas por el Administrador de controladores y ordena los registros de estado que genera. (Un ODBC 2. *x* controlador no ordena los registros de estado.) Esto incluye errores y advertencias de truncamiento de datos, la conversión de datos, la sintaxis y algunas transiciones de estado. También puede comprobar el controlador de errores y advertencias parcialmente activadas por el Administrador de controladores. Por ejemplo, aunque el Administrador de controladores comprueba si el valor de *operación* en **SQLSetPos** es válida, el controlador debe comprobar si se admite.  
  
 El controlador también asigna *errores nativos* : es decir, los errores devueltos por el origen de datos: para SQLSTATE. Por ejemplo, el controlador puede asignar un número de errores nativos diferentes para la sintaxis SQL no válida para SQLSTATE 42000 (sintaxis o infracción de acceso). El controlador devuelve el número de error nativo en el campo SQL_DIAG_NATIVE del registro de estado. Documentación del controlador debe mostrar cómo errores y advertencias se asignan desde el origen de datos a los argumentos en **SQLGetDiagRec** y **SQLGetDiagField**.

