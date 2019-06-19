---
title: Asignación de SQLTransact | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5cf669883ce81528adbe1fbd8faeff2ed716218
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735143"
---
# <a name="sqltransact-mapping"></a>Asignación de SQLTransact
**SQLTransact** ahora se reemplaza por **SQLEndTran**. Es la principal diferencia entre las dos funciones que **SQLEndTran** contiene un argumento *HandleType*, que especifica el ámbito de la que se realice el trabajo. El *HandleType* argumento puede especificar el entorno o el identificador de conexión. La siguiente llamada a **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 se asigna a  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 Si *ConnectionHandle* no es igual a SQL_NULL_HDBC. El *ConnectionHandle* argumento está establecido en el valor de *hdbc*.  
  
 **SQL_Transact** está asignado a  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 Si *ConnectionHandle* es igual a SQL_NULL_HDBC. El *EnvironmentHandle* argumento está establecido en el valor de *henv*.  
  
 En ambos de los casos anteriores, el *Sql_commit* argumento está establecido en el mismo valor que *fType*.
