---
title: Asignación de SQLBindParam ( SQLBindParam Mapping) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1df595722297c91dc75398470912188e109e278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305445"
---
# <a name="sqlbindparam-mapping"></a>Asignación de SQLBindParam
**SQLBindParam** no se puede llamar realmente en desuso porque nunca estuvo allí en ODBC; sin embargo, todavía representa la funcionalidad duplicada - el Administrador de controladores necesita exportarlo porque las aplicaciones compatibles con ISO y Open Group lo utilizarán. Dado que **SQLBindParameter** contiene toda la funcionalidad de **SQLBindParam**, **SQLBindParam** se asignará encima de **SQLBindParameter** (cuando el controlador subyacente es un controlador ODBC *3.x).* Un controlador ODBC *3.x* no necesita implementar **SQLBindParam**.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se realiza la siguiente llamada a **SQLBindParam:**  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 el Administrador de controladores llama **a SQLBindParameter** en el controlador de la siguiente manera:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Consulte Información de [ODBC de 64 bits,](../../../odbc/reference/odbc-64-bit-information.md)si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
## <a name="see-also"></a>Consulte también  
 [Asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
