---
title: Asignación de SQLSetParam | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300535"
---
# <a name="sqlsetparam-mapping"></a>Asignación de SQLSetParam
**SQLSetParam** se sigue asignando en la parte superior de **SQLBindParameter** , como en ODBC 2. *x*. Aunque es conceptualmente similar a **SQLBindParam**, el administrador de controladores no asigna **SQLSetParam** a **SQLBindParam**. Esto se debe a que hay ODBC 2 existente. los controladores *x* usan el valor especial de *BufferLength* (SQL_SETPARAM_VALUE_MAX) que genera el administrador de controladores cuando asigna **SQLSetParam** en la parte superior de **SQLBindParameter** para determinar cuándo lo llama un 1. aplicación ODBC *x* .  
  
 Una llamada a  
  
```  
SQLSetParam(hstmt, ipar, fCType, fSqlType, cbColDef, ibScale, rgbValue, pcbValue)  
```  
  
 dará como resultado lo siguiente:  
  
```  
SQLBindParameter(StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, ColumnSize, DecimalDigits, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr)  
```
