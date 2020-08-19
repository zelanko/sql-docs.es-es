---
description: Ejemplo de la propiedad de estado (campo) (VB)
title: Ejemplo de la propiedad de estado (campo) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 66fab5cee49adf89bffee79f5b51b13780d5d982
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441947"
---
# <a name="status-property-example-field-vb"></a>Ejemplo de la propiedad de estado (campo) (VB)
En el ejemplo siguiente se abre un documento desde una carpeta de lectura/escritura mediante el [proveedor de publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). La propiedad [status](../../../ado/reference/ado-api/status-property-ado-field.md) de un objeto [Field](../../../ado/reference/ado-api/field-object.md) del [registro](../../../ado/reference/ado-api/record-object-ado.md) se establecerá primero en **adFieldPendingInsert**y, a continuación, se actualizará a **adFieldOk**.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 En el ejemplo siguiente se elimina un **campo** conocido de un **registro** abierto desde un documento. La propiedad **status** se establecerá primero en **adFieldOK**y luego en **adFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 El código siguiente elimina un **campo** de un **registro** abierto en un documento de solo lectura. **Status** se establecerá en **adFieldPendingDelete**. En la [actualización](../../../ado/reference/ado-api/update-method.md), se producirá un error en la eliminación y el **Estado** será **adFieldPendingDelete** más **adFieldPermissionDenied**. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) borra la configuración de **Estado** pendiente.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Consulte también  
 [Field (objeto)](../../../ado/reference/ado-api/field-object.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Propiedad Status (Field ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
