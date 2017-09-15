---
title: "Asignación de SQLAllocStmt | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8361f0b77e8f15f775eece7aae9b599be5e62ac
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlallocstmt-mapping"></a>Asignación de SQLAllocStmt
Cuando una aplicación llama **SQLAllocStmt** a través de una aplicación ODBC 3*.x* controlador, la llamada a:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 se asigna a **SQLAllocHandle** por el Administrador de controladores en el controlador de la manera siguiente:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 con *InputHandle* establecido en *hdbc* y *OutputHandlePtr* establecido en *phstmt*.
