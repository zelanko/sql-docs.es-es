---
title: Función SQLRemoveDefaultDataSource | Documentos de Microsoft
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
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed9d4bbed89bc4ed9330e8e857dcf1a0b9a3c149
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedefaultdatasource-function"></a>SQLRemoveDefaultDataSource (función)
**Conformidad**  
 Versión introdujo: ODBC 1.0, en desuso  
  
 **Resumen**  
 En ODBC 3.0, el **SQLRemoveDefaultDataSource** función se ha reemplazado por una llamada a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con una *fRequest* argumento de ODBC_REMOVE_DEFAULT_DSN. Si una API ODBC 2 *.x* programa de instalación llama a esta función, el instalador ODBC asignará al siguiente **SQLConfigDataSource** llamar:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
