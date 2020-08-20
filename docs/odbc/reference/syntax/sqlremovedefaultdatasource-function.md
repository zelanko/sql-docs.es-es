---
description: Función SQLRemoveDefaultDataSource
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0010e59cc4dfad2d54b8b1c4e59e83ea72fcd3ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487093"
---
# <a name="sqlremovedefaultdatasource-function"></a>Función SQLRemoveDefaultDataSource
**Conformidad**  
 Versión introducida: ODBC 1,0, en desuso  
  
 **Resumen**  
 En ODBC 3,0, la función **SQLRemoveDefaultDataSource** se ha reemplazado por una llamada a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con un argumento *fRequest* de ODBC_REMOVE_DEFAULT_DSN. Si un programa de instalación de ODBC 2 *. x* llama a esta función, el instalador de ODBC la asignará a la siguiente llamada a **SQLConfigDataSource** :  
  
```cpp  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
