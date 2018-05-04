---
title: Asignación de SQLError | Documentos de Microsoft
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
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ba54875173e6836279db6c043a017af8a191dae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlerror-mapping"></a>Asignación de SQLError
Cuando una aplicación llama **SQLError** a través de una aplicación ODBC 3 *.x* controlador, la llamada a  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 se asigna a  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 con el *HandleType* argumento establecido en el valor SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT, según corresponda y el *controlar* establecido en el valor de *henv*, *hdbc*, o *hstmt*, según corresponda. El *RecNumber* argumento se determina por el Administrador de controladores.
