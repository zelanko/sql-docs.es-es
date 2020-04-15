---
title: Asignación de SQLTransact (SQLTransact Mapping) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aaa056fca860a70f81ad7c3a4cd8539512bc25d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304886"
---
# <a name="sqltransact-mapping"></a>Asignación de SQLTransact
**SQLTransact** ahora se reemplaza por **SQLEndTran**. La principal diferencia entre las dos funciones es que **SQLEndTran** contiene un argumento *HandleType*, que especifica el ámbito del trabajo que se va a realizar. El *HandleType* argumento puede especificar el entorno o el identificador de conexión. La siguiente llamada a **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 se asigna a  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 si *ConnectionHandle* no es igual a SQL_NULL_HDBC. El argumento *ConnectionHandle* se establece en el valor de *hdbc*.  
  
 **SQL_Transact** se asigna a  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 si *ConnectionHandle* es igual a SQL_NULL_HDBC. El *argumento EnvironmentHandle* se establece en el valor de *henv*.  
  
 En los dos casos anteriores, el argumento *CompletionType* se establece en el mismo valor *que fType*.
