---
title: "Asignación de SQLSetParam | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: adebe26728690a6d631ca94e8ce11040ebc08a0f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetparam-mapping"></a>Asignación de SQLSetParam
**SQLSetParam** continúa asignarse en la parte superior de **SQLBindParameter** como en ODBC 2. *x*. Aunque es conceptualmente similar a **SQLBindParam**, el Administrador de controladores no se asigna **SQLSetParam** a **SQLBindParam**. Esto es porque cierto 2 de ODBC existente. *x* controladores utilizan el valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que el Administrador de controladores que se genera cuando se asigna **SQLSetParam** sobre  **SQLBindParameter** para determinar cuando se llama mediante un 1. *x* aplicación ODBC.  
  
 Una llamada a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 se producirá lo siguiente:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
