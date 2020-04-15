---
title: SQLRemoveDefaultDataSource (Función) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 952ace7d17e8bb5b4c824761b02e5c8a0895f519
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303946"
---
# <a name="sqlremovedefaultdatasource-function"></a>Función SQLRemoveDefaultDataSource
**Conformidad**  
 Versión introducida: ODBC 1.0, en desuso  
  
 **Resumen**  
 En ODBC 3.0, la función **SQLRemoveDefaultDataSource** se ha reemplazado por una llamada a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con un argumento *fRequest* de ODBC_REMOVE_DEFAULT_DSN. Si un programa de instalación ODBC 2 *.x* llama a esta función, el instalador ODBC la asignará a la siguiente llamada **SQLConfigDataSource:**  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
