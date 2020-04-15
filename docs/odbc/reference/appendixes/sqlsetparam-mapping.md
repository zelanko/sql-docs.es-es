---
title: Asignación de SQLSetParam ( SQLSetParam) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8e632412965664e5cdd9c87dc1e26787dcdab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300535"
---
# <a name="sqlsetparam-mapping"></a>Asignación de SQLSetParam
**SQLSetParam** continúa mapeándose encima de **SQLBindParameter** como en ODBC 2. *x*. Aunque es conceptualmente similar a **SQLBindParam**, el Administrador de controladores no asigna **SQLSetParam** a **SQLBindParam**. Esto se debe a que ciertoODBC 2 existente. *x* controladores utilizan el valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que el Administrador de controladores genera cuando asigna **SQLSetParam** encima de **SQLBindParameter** para determinar cuándo se llama por un 1. *x* Aplicación ODBC.  
  
 Una llamada a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 dará lugar a lo siguiente:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
