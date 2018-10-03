---
title: La habilitación del seguimiento | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: fb6d8eaf4a1f4eaadc4e8e9a7030b81c373d8377
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819923"
---
# <a name="enabling-tracing"></a>La habilitación del seguimiento
Seguimiento se puede habilitar en las siguientes tres formas:  
  
-   Establecer el **seguimiento** y **TraceFile** palabras clave en la entrada de registro del archivo Odbc.ini. Esto habilita o deshabilita el seguimiento cuando **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV se llama. Estas opciones se establecen en la ficha trazas del cuadro de diálogo Administrador de orígenes de datos ODBC muestra durante la instalación de origen de datos. Para obtener más información, consulte [entradas del registro de orígenes de datos](../../../odbc/reference/install/registry-entries-for-data-sources.md).  
  
-   Llame a **SQLSetConnectAttr** para establecer el atributo de conexión SQL_ATTR_TRACE en SQL_OPT_TRACE_ON. Esto habilita o deshabilita el seguimiento de la duración de la conexión. Para obtener más información, consulte el [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) descripción de la función.  
  
-   Use **ODBCSharedTraceFlag** para activar o desactivar el seguimiento de forma dinámica. (Para obtener más información, vea el tema siguiente, [seguimiento dinámico](../../../odbc/reference/develop-app/dynamic-tracing.md).)
