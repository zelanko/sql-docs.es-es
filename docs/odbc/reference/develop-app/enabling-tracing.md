---
title: Habilitando el seguimiento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24f80e0e81e4be8895d59256492b868c53aab7b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046793"
---
# <a name="enabling-tracing"></a>La habilitación del seguimiento
El seguimiento se puede habilitar de las tres maneras siguientes:  
  
-   Establezca **las palabras clave Trace y de** **seguimiento** en la entrada del registro ODBC. ini. Esto habilita o deshabilita el seguimiento cuando se llama a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV. Estas opciones se establecen en la pestaña seguimiento del cuadro de diálogo Administrador de orígenes de datos ODBC que se muestra durante la configuración del origen de datos. Para obtener más información, vea [entradas del registro para orígenes de datos](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Llame a **SQLSetConnectAttr** para establecer el atributo de conexión SQL_ATTR_TRACE en SQL_OPT_TRACE_ON. Esto habilita o deshabilita el seguimiento mientras dure la conexión. Para obtener más información, consulte la descripción de la función [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) .  
  
-   Use **ODBCSharedTraceFlag** para activar o desactivar el seguimiento de forma dinámica. (Para obtener más información, vea el tema siguiente, [seguimiento dinámico](../../../odbc/reference/develop-app/dynamic-tracing.md)).
