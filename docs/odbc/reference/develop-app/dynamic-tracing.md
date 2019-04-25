---
title: Seguimiento dinámico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], dynamic
- dynamic tracing [ODBC]
ms.assetid: ebe58a83-a7b0-4747-86c8-2af2940471ef
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63dbfda01d96cad53e5830e598b5812ed79d8f04
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468782"
---
# <a name="dynamic-tracing"></a>Seguimiento dinámico
El seguimiento se puede habilitar o deshabilitar en cualquier momento en una ejecución de la aplicación. Esto permite que una aplicación para realizar un seguimiento de cualquier número de llamadas de función.  
  
 La variable **ODBCSharedTraceFlag** se establece para habilitar el seguimiento de forma dinámica. Esta variable se comparte entre todas las copias de ejecución del Administrador de controladores. Si cualquier aplicación establece esta variable, el seguimiento está habilitado para todas las aplicaciones ODBC que se está ejecutando actualmente. Para desactivar el seguimiento desactivado cuando está habilitado el seguimiento dinámico, una aplicación llama a **SQLSetConnectAttr** establecer SQL_ATTR_TRACE en SQL_TRACE_OFF. Esta llamada se activará el seguimiento desactivado para esa aplicación solo. Las aplicaciones que están vinculadas con Odbc32.lib pueden modificar el uso de esta variable. Datos de seguimiento pueden mostrarse en una ventana en tiempo real, en lugar del archivo de seguimiento, que se debe abrir después de la sesión ODBC. Pueden agregarse controles en pantalla de la aplicación para activar o desactivar el seguimiento en le.  
  
 El seguimiento de la DLL se incluye con ODBC 3 *.x* no es segura para subprocesos. No se garantiza que el archivo de registro se escribe correctamente si se habilita el seguimiento global (la variable **ODBCSharedTraceFlag** está establecido) y más de una aplicación escribe en el archivo de seguimiento al mismo tiempo. Esta condición no devuelve un error.
