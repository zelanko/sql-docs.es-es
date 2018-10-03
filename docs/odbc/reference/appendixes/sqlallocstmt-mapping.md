---
title: Asignación de SQLAllocStmt | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 330c245d8b5839fd8a721a7399a22edea78a2417
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47819973"
---
# <a name="sqlallocstmt-mapping"></a>Asignación de SQLAllocStmt
Cuando una aplicación llama **SQLAllocStmt** a través de una aplicación ODBC 3 *.x* controlador, la llamada a:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 se asigna a **SQLAllocHandle** por el Administrador de controladores en el controlador como sigue:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 con *InputHandle* establecido en *hdbc* y *OutputHandlePtr* establecido en *phstmt*.
