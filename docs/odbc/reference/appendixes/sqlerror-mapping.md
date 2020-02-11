---
title: Asignación de SQLError | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLError
- SQLError function [ODBC], mapping
ms.assetid: 802ac711-7e5d-4152-9698-db0cafcf6047
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f24a305c2f22ef4cfacbbe4bcbcf498eab648f1c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064474"
---
# <a name="sqlerror-mapping"></a>Asignación de SQLError
Cuando una aplicación llama a **SQLError** a través de un controlador ODBC *3. x* , la llamada a  
  
```  
SQLError(henv, hdbc, hstmt, szSqlState, pfNativeError, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)   
```  
  
 está asignado a  
  
```  
SQLGetDiagRec(HandleType, Handle, RecNumber, szSqlstate, pfNativeErrorPtr, szErrorMsg, cbErrorMsgMax, pcbErrorMsg)  
```  
  
 con el argumento *HandleType* establecido en el valor SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT, según corresponda, y el argumento *Handle* establecido en el valor de *HENV*, *hdbc*o *hstmt*, según corresponda. El argumento *RecNumber* viene determinado por el administrador de controladores.
