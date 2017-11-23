---
title: "La habilitación del seguimiento | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 569c5b42c57bca4eff30225f5dcc1ff1176fe00e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="enabling-tracing"></a>La habilitación del seguimiento
El seguimiento se puede habilitar en las siguientes tres formas:  
  
-   Establecer el **seguimiento** y **TraceFile** palabras clave en la entrada de registro Odbc.ini. Esto habilita o deshabilita el seguimiento cuando **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se denomina. Estas opciones se establecen en la ficha trazas del cuadro de diálogo Administrador de orígenes de datos ODBC que se muestra durante la instalación de origen de datos. Para obtener más información, consulte [entradas del registro para los orígenes de datos](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Llame a **SQLSetConnectAttr** para establecer el atributo de conexión SQL_ATTR_TRACE en SQL_OPT_TRACE_ON. Esto habilita o deshabilita el seguimiento de la duración de la conexión. Para obtener más información, consulte el [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descripción de la función.  
  
-   Use **ODBCSharedTraceFlag** para activar o desactivar el seguimiento dinámicamente. (Para obtener más información, vea el tema siguiente, [seguimiento dinámico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
