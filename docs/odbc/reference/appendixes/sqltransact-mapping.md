---
title: Asignación de SQLTransact | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLTransact
- SQLTransact function [ODBC], mapping
ms.assetid: 8a01041f-3572-46f9-8213-b817f3cf929c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e938a4eb7c605d1ed9cf71c038bcc7187e1a8cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqltransact-mapping"></a>Asignación de SQLTransact
**SQLTransact** ha sido sustituida por **SQLEndTran**. La principal diferencia entre las dos funciones es que **SQLEndTran** contiene un argumento *HandleType*, que especifica el ámbito del trabajo en realizarse. El *HandleType* argumento puede especificar el entorno o el identificador de conexión. La siguiente llamada a **SQLTransact**:  
  
```  
SQLTransact(henv, hdbc, fType)  
```  
  
 se asigna a  
  
```  
SQLEndTran(SQL_HANDLE_DBC, ConnectionHandle, CompletionType);  
```  
  
 Si *IdentificadorConexión* no es igual a SQL_NULL_HDBC. El *IdentificadorConexión* argumento tiene asignado el valor de *hdbc*.  
  
 **SQL_Transact** se asigna a  
  
```  
SQLEndTran (SQL_HANDLE_ENV, EnvironmentHandle, CompletionType);  
```  
  
 Si *IdentificadorConexión* es igual a SQL_NULL_HDBC. El *EnvironmentHandle* argumento tiene asignado el valor de *henv*.  
  
 En ambos de los casos anteriores, el *Sql_commit* argumento tiene asignado el mismo valor que *fType*.
