---
title: "Asignación de SQLBindParam | Documentos de Microsoft"
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
- SQLBindparam function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLBindParam
ms.assetid: 375f8f24-36de-4946-916e-c75abc6f070d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d94cdc4b73bd176ae7af002ab290b795ad87d39e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparam-mapping"></a>Asignación de SQLBindParam
**SQLBindParam** no se puede llamar realmente en desuso porque no estaba presente en ODBC; sin embargo, todavía representa funcionalidad duplicada, debe exportarlo ya ISO y abra compatible con grupo de aplicaciones se va a usar el Administrador de controladores. Dado que **SQLBindParameter** contiene toda la funcionalidad de **SQLBindParam**, **SQLBindParam** va a asignar sobre **SQLBindParameter** (cuando el controlador subyacente es una aplicación ODBC 3*.x* controlador). Una aplicación ODBC 3*.x* controlador no es necesario implementar **SQLBindParam**.  
  
## <a name="remarks"></a>Comentarios  
 Cuando la siguiente llamada a **SQLBindParam** se realiza:  
  
```  
SQLBindParam(   StatementHandle,    ParameterNumber,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    StrLen_or_IndPtr)  
```  
  
 las llamadas del Administrador de controladores **SQLBindParameter** en el controlador de la manera siguiente:  
  
```  
SQLBindParameter(   StatementHandle,    ParameterNumber,    SQL_PARAM_INPUT,    ValueType,    ParameterType,    ColumnSize,    DecimalDigits,    ParameterValuePtr,    BufferLength,    StrLen_or_IndPtr)  
```  
  
 Vea [información ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
## <a name="see-also"></a>Vea también  
 [Asignación de funciones en desuso.](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)

