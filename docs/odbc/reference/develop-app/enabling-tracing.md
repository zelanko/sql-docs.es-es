---
title: Habilitación del seguimiento de la aplicación de la aplicación de Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287355"
---
# <a name="enabling-tracing"></a>La habilitación del seguimiento
El seguimiento se puede habilitar de las tres maneras siguientes:  
  
-   Establezca las palabras clave **Trace** y **TraceFile** en la entrada del Registro Odbc.ini. Esto habilita o deshabilita el seguimiento cuando **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se llama. Estas opciones se establecen en la pestaña Seguimiento del cuadro de diálogo Administrador de orígenes de datos ODBC que se muestra durante la instalación del origen de datos. Para obtener más información, consulte [Entradas del Registro para orígenes de datos](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Llame a **SQLSetConnectAttr** para establecer el atributo de conexión SQL_ATTR_TRACE en SQL_OPT_TRACE_ON. Esto habilita o deshabilita el seguimiento durante la conexión. Para obtener más información, vea la descripción de la función [SQLSetConnectAttr.](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   Use **ODBCSharedTraceFlag** para activar o desactivar el seguimiento dinámicamente. (Para obtener más información, consulte el tema siguiente, [Seguimiento dinámico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
