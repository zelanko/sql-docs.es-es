---
title: "La habilitación del seguimiento | Documentos de Microsoft"
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
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d80f7e70915c11a3a45f90d2821b9c1bd137d9dd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="enabling-tracing"></a>La habilitación del seguimiento
El seguimiento se puede habilitar en las siguientes tres formas:  
  
-   Establecer el **seguimiento** y **TraceFile** palabras clave en la entrada de registro Odbc.ini. Esto habilita o deshabilita el seguimiento cuando **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se denomina. Estas opciones se establecen en la ficha trazas del cuadro de diálogo Administrador de orígenes de datos ODBC que se muestra durante la instalación de origen de datos. Para obtener más información, consulte [entradas del registro para los orígenes de datos](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Llame a **SQLSetConnectAttr** para establecer el atributo de conexión SQL_ATTR_TRACE en SQL_OPT_TRACE_ON. Esto habilita o deshabilita el seguimiento de la duración de la conexión. Para obtener más información, consulte el [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descripción de la función.  
  
-   Use **ODBCSharedTraceFlag** para activar o desactivar el seguimiento dinámicamente. (Para obtener más información, vea el tema siguiente, [seguimiento dinámico](../../../odbc/reference/develop-app/dynamic-tracing.md).)

