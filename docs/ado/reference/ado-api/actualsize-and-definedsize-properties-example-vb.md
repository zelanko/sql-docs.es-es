---
description: Ejemplo de propiedades ActualSize y DefinedSize (VB)
title: Ejemplo de propiedades ActualSize y DefinedSize (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- DefinedSize property [ADO], Visual Basic example
- ActualSize property [ADO], Visual Basic example
ms.assetid: bff2c273-b535-4b32-83b3-0336a406859c
author: rothja
ms.author: jroth
ms.openlocfilehash: 67fd214c594a808955e54edbb9ccb4e7d424e836
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976936"
---
# <a name="actualsize-and-definedsize-properties-example-vb"></a>Ejemplo de propiedades ActualSize y DefinedSize (VB)
En este ejemplo se usan las propiedades [ActualSize](./actualsize-property-ado.md) y [DefinedSize](./definedsize-property.md) para mostrar el tamaño definido y el tamaño real de un campo.  
  
```vb
'BeginActualSizeVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstStores As ADODB.Recordset  
    Dim SQLStores As String  
    Dim strCnxn As String  
     'record variables  
    Dim strMessage As String  
  
    ' Open a recordset for the Stores table  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Northwind';Integrated Security='SSPI';"  
    Set rstStores = New ADODB.Recordset  
  
    SQLStores = "Suppliers"  
    rstStores.Open SQLStores, strCnxn, adOpenForwardOnly, adLockReadOnly, adCmdTable  
    'the above two lines of code are identical as the default values for  
    'CursorType and LockType arguments match those indicated  
  
    ' Loop through the recordset displaying the contents  
    ' of the store_name field, the field's defined size,  
    ' and its actual size.  
    rstStores.MoveFirst  
  
    Do Until rstStores.EOF  
        strMessage = "Company name: " & rstStores!CompanyName & _  
        vbCrLf & "Defined size: " & _  
        rstStores!CompanyName.DefinedSize & _  
        vbCrLf & "Actual size: " & _  
        rstStores!CompanyName.ActualSize & vbCrLf  
  
        MsgBox strMessage, vbOKCancel, "ADO ActualSize Property (Visual Basic)"  
        rstStores.MoveNext  
    Loop  
  
    ' clean up  
    rstStores.Close  
    Set rstStores = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstStores Is Nothing Then  
        If rstStores.State = adStateOpen Then rstStores.Close  
    End If  
    Set rstStores = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActualSizeVB  
```  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad ActualSize (ADO)](./actualsize-property-ado.md)   
 [Propiedad DefinedSize](./definedsize-property.md)   
 [Objeto Field](./field-object.md)