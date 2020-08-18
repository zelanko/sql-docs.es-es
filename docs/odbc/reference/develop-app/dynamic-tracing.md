---
description: Seguimiento dinámico
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1618d1b2837c5169f03b07900aba3921bc98659
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482998"
---
# <a name="dynamic-tracing"></a>Seguimiento dinámico
El seguimiento se puede habilitar o deshabilitar en cualquier momento de la ejecución de una aplicación. Esto permite que una aplicación pueda realizar un seguimiento de cualquier número de llamadas de función.  
  
 La variable **ODBCSharedTraceFlag** se establece para habilitar el seguimiento de forma dinámica. Esta variable se comparte entre todas las copias en ejecución del administrador de controladores. Si alguna aplicación establece esta variable, el seguimiento se habilita para todas las aplicaciones ODBC que se están ejecutando actualmente. Para desactivar el seguimiento cuando se habilita el seguimiento dinámico, una aplicación llama a **SQLSetConnectAttr** para establecer SQL_ATTR_TRACE en SQL_TRACE_OFF. Esta llamada activará el seguimiento solo para esa aplicación. Las aplicaciones que están vinculadas con odbc32. lib pueden modificar el uso de esta variable. Los datos de seguimiento se pueden mostrar en una ventana en tiempo real, en lugar del archivo de seguimiento, que se debe abrir después de la sesión ODBC. Se pueden agregar controles a la pantalla de una aplicación para activar o desactivar el seguimiento en.  
  
 La DLL de seguimiento suministrada con ODBC 3 *. x* no es segura para subprocesos. No se garantiza que el archivo de registro se escriba correctamente si está habilitado el seguimiento global (se establece la variable **ODBCSharedTraceFlag** ) y más de una aplicación escribe en el archivo de seguimiento al mismo tiempo. Esta condición no devuelve un error.
