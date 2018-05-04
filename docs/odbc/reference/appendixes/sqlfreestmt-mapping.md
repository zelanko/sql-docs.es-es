---
title: Asignación de SQLFreeStmt | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeStmt
ms.assetid: 267d95f2-4f0c-47ab-9411-5afe105215a2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77392dff0f22fcabd26b54cad700bb5cebcde2bf
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlfreestmt-mapping"></a>Asignación de SQLFreeStmt
Cuando una aplicación llama **SQLFreeStmt** con una *opción* argumento de SQL_DROP a través de una aplicación ODBC 3 *.x* controlador, la llamada a  
  
```  
SQLFreeStmt(hstmt, SQL_DROP)   
```  
  
 se asigna a  
  
```  
SQLFreeHandle(SQL_HANDLE_STMT,Handle)  
```  
  
 con el *controlar* establecido en el valor de *hstmt*.
