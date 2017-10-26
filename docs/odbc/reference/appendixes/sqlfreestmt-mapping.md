---
title: "Asignación de SQLFreeStmt | Documentos de Microsoft"
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
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: df3cfba17f19074fbe00f33ef7fba098a4fe8184
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreestmt-mapping"></a>Asignación de SQLFreeStmt
Cuando una aplicación llama **SQLFreeStmt** con una *opción* argumento de SQL_DROP a través de una aplicación ODBC 3*.x* controlador, la llamada a  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 se asigna a  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 con el *controlar* establecido en el valor de *hstmt*.

