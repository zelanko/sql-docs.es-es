---
title: Asignación de SQLBindParam | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ecec6116ee16f4affa615518a690d2c665648464
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091243"
---
# <a name="sqlbindparam-mapping"></a>Asignación de SQLBindParam
**SQLBindParam** no realmente se puede llamar en desuso porque no existe en ODBC; sin embargo, todavía representa funcionalidad duplicada: debe exportarlo porque ISO y abierto compatible con grupo de aplicaciones lo va a usar el Administrador de controladores. Dado que **SQLBindParameter** contiene toda la funcionalidad de **SQLBindParam**, **SQLBindParam** se asignará en la parte superior de **SQLBindParameter** (cuando el controlador subyacente es un ODBC *3.x* controlador). Un ODBC *3.x* no es necesario implementar controladores **SQLBindParam**.  
  
## <a name="remarks"></a>Comentarios  
 Cuando la llamada siguiente a **SQLBindParam** se realiza:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 las llamadas del Administrador de controladores **SQLBindParameter** en el controlador como sigue:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Consulte [información ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md), si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
## <a name="see-also"></a>Vea también  
 [Asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)
