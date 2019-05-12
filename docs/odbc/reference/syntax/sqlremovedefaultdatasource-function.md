---
title: Función SQLRemoveDefaultDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea540d2ef6747bbe3bfc9ac55f04afe1d63349f7
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537241"
---
# <a name="sqlremovedefaultdatasource-function"></a>Función SQLRemoveDefaultDataSource
**Conformidad**  
 Versión de introducción: ODBC 1.0, en desuso  
  
 **Resumen**  
 En ODBC 3.0, el **SQLRemoveDefaultDataSource** función ha sido reemplazada por una llamada a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con un *fRequest* argumento de ODBC_REMOVE_DEFAULT_DSN. Si un ODBC 2 *.x* programa de instalación llama a esta función, el instalador ODBC asignará al siguiente **SQLConfigDataSource** llamar:  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
