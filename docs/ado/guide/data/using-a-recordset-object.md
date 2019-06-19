---
title: Uso de un objeto Recordset | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5fc27ed728483fd42d90e599580ce32194f08b99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699898"
---
# <a name="using-a-recordset-object"></a>Mediante un objeto de conjunto de registros
Como alternativa, puede usar **Recordset.Open** para establecer una conexión y emitir un comando a través de esa conexión en una sola operación de forma implícita. Por ejemplo, en Visual Basic:  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 Tenga en cuenta que **oRs.Open** toma una cadena de conexión (*sConn*), en lugar de un **conexión** objeto (*oConn*), como el valor de su  **ActiveConnection** parámetro. También se aplica el tipo de cursor del lado cliente estableciendo el **CursorLocation** propiedad en el **Recordset** objeto. De nuevo, Compare esto con el **HelloData** ejemplo.
