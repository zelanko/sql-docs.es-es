---
title: Seguimiento dinámico | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6746566d09d2862275daf508d08e20e2fca8473
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="dynamic-tracing"></a>Seguimiento dinámico
Seguimiento se puede habilitar o deshabilitar en cualquier momento en una ejecución de la aplicación. Esto permite que una aplicación realizar el seguimiento de cualquier número de llamadas de función.  
  
 La variable **ODBCSharedTraceFlag** se establece para habilitar el seguimiento de forma dinámica. Esta variable se comparte entre todas las copias de ejecución del Administrador de controladores. Si cualquier aplicación establece esta variable, el seguimiento está habilitado para todas las aplicaciones de ODBC que se está ejecutando actualmente. Para desactivar el seguimiento desactivado cuando está habilitado el seguimiento dinámico, una aplicación llama **SQLSetConnectAttr** para establecer SQL_ATTR_TRACE en SQL_TRACE_OFF. Esta llamada se desactivará seguimiento desactivado para dicha aplicación únicamente. Las aplicaciones que están vinculadas con Odbc32.lib pueden modificar el uso de esta variable. Los datos de seguimiento se pueden mostrar en una ventana en tiempo real, en lugar del archivo de seguimiento, que debe estar abierto después de la sesión ODBC. Pueden agregarse controles en pantalla de la aplicación para activar o desactivar el seguimiento en le.  
  
 El seguimiento de la DLL que se incluye con ODBC 3 *.x* no es segura para subprocesos. No se garantiza que el archivo de registro se escribe correctamente si se habilita el seguimiento global (la variable **ODBCSharedTraceFlag** está establecido) y más de una aplicación escribe en el archivo de seguimiento al mismo tiempo. Esta condición no devuelve un error.
