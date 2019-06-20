---
title: SQLSetParam Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetParam
- SQLSetParam function [ODBC], mapping
ms.assetid: 022dfbc0-8d18-4c35-8a28-d9eb16063188
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5d420bc68c4704705018a37c6459181481b1d7d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297472"
---
# <a name="sqlsetparam-mapping"></a>Asignación de SQLSetParam
**SQLSetParam** continúa asignarse en la parte superior de **SQLBindParameter** como en ODBC 2. *x*. Aunque es conceptualmente similar a **SQLBindParam**, no se asigna el Administrador de controladores **SQLSetParam** a **SQLBindParam**. Esto es porque cierto 2 de ODBC existente. *x* controladores utilizan el valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que el Administrador de controladores que se genera cuando se asigna **SQLSetParam** en la parte superior de  **SQLBindParameter** para determinar cuando se llama mediante un 1. *x* aplicación ODBC.  
  
 Una llamada a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 se producirá lo siguiente:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
