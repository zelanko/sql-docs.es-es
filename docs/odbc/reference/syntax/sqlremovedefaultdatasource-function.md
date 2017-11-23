---
title: "Función SQLRemoveDefaultDataSource | Documentos de Microsoft"
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
apiname: SQLRemoveDefaultDataSource
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRemoveDefaultDataSource
helpviewer_keywords: SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d8b1e368c3ed09b0cc99de6b324a02546e04803e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource (función)
**Conformidad**  
 Versión introdujo: ODBC 1.0, en desuso  
  
 **Resumen**  
 En ODBC 3.0, el **SQLRemoveDefaultDataSource** función se ha reemplazado por una llamada a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con una *fRequest* argumento de ODBC_REMOVE_DEFAULT_DSN. Si una API ODBC 2*.x* programa de instalación llama a esta función, el instalador ODBC asignará al siguiente **SQLConfigDataSource** llamar:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
