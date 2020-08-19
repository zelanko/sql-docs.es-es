---
description: Comandos con nombre
title: Comandos con nombre | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO]
ms.assetid: 5a0ec8f9-5ba3-4f9f-b80d-2073aa049586
author: rothja
ms.author: jroth
ms.openlocfilehash: 607142ec89a1032fe42bab87c0dfad0f2a276387
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453157"
---
# <a name="named-commands"></a>Comandos con nombre
[La creación y ejecución de un comando simple](../../../ado/guide/data/creating-and-executing-a-simple-command.md) muestra una manera de ejecutar un comando. Hay otra manera: puede convertirla en un comando con nombre y, a continuación, llamar a este comando con nombre directamente en el objeto de **conexión** (asignado a la propiedad **ActiveConnection** del objeto **Command** ). El nombre de un comando significa asignar un nombre a la propiedad **Name** de un objeto **Command** . Por ejemplo,  
  
```  
objCmd.Name = "GetCustomers"  
objCmd.ActiveConnection = objConn  
objConn.GetCustomers objRs  
```  
  
 El comando con nombre actúa como si fuera un "método personalizado" en el objeto de **conexión** . El resultado del comando se devuelve como un parámetro out de este "método personalizado".  
  
 En el ejemplo siguiente se muestra esta característica.  
  
```  
'BeginNamedCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
  
    objCmd.CommandText = "SELECT CustomerID, CompanyName FROM Customers"  
    objCmd.CommandType = adCmdText  
  
    'Name the command.  
    objCmd.Name = "GetCustomers"  
  
    objCmd.ActiveConnection = objConn  
  
    ' Execute using Command.Name from the Connection.  
    objConn.GetCustomers objRs  
  
    ' Display.  
    Do While Not objRs.EOF  
        Debug.Print objRs(0) & vbTab & objRs(1)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndNamedCmd  
```  
  
## <a name="see-also"></a>Consulte también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
