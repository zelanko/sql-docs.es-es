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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 447233a3ba014a5ef92f2f49840ad302f8aeccf0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305488"
---
# <a name="sqlallocstmt-mapping"></a>Asignación de SQLAllocStmt
Cuando una aplicación llama a **SQLAllocStmt** a través de un controlador ODBC *3. x* , la llamada a:  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 lo asigna el **Administrador de controladores** en el controlador de la manera siguiente:  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 con *InputHandle* establecido en *hdbc* y *OutputHandlePtr* establecido en *phstmt*.
