---
title: Seguimiento dinámico de la página de seguimiento dinámico de la página Microsoft Docs
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
ms.openlocfilehash: 8cbd2dbae4f4b437f45845ce2791f4a9b0aa8c8b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305775"
---
# <a name="dynamic-tracing"></a>Seguimiento dinámico
El seguimiento se puede habilitar o deshabilitar en cualquier punto de una ejecución de aplicación. Esto permite a una aplicación rastrear cualquier número de llamadas de función.  
  
 La variable **ODBCSharedTraceFlag** se establece para habilitar el seguimiento dinámicamente. Esta variable se comparte entre todas las copias en ejecución del Administrador de controladores. Si alguna aplicación establece esta variable, el seguimiento está habilitado para todas las aplicaciones ODBC que se ejecutan actualmente. Para desactivar el seguimiento cuando se habilita el seguimiento dinámico, una aplicación llama a **SQLSetConnectAttr** para establecer SQL_ATTR_TRACE en SQL_TRACE_OFF. Esta llamada desactivará el seguimiento solo para esa aplicación. Las aplicaciones vinculadas con Odbc32.lib pueden modificar el uso de esta variable. Los datos de seguimiento se pueden mostrar en una ventana en tiempo real, en lugar del archivo de seguimiento, que debe abrirse después de la sesión ODBC. Los controles se pueden agregar a la pantalla de una aplicación para activar o desactivar el seguimiento a voluntad.  
  
 El archivo DLL de seguimiento incluido con ODBC 3 *.x* no es seguro para subprocesos. No se garantiza que el archivo de registro se escribe correctamente si el seguimiento global está habilitado (la variable **ODBCSharedTraceFlag** está establecida) y más de una aplicación escribe en el archivo de seguimiento al mismo tiempo. Esta condición no devuelve un error.
