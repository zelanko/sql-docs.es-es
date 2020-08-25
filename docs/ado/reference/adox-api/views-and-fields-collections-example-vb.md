---
description: Ejemplo de colecciones de vistas y campos (VB)
title: Ejemplo de colecciones y campos de vistas (VB) | Microsoft Docs
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
- Views collection [ADOX], Visual Basic example
- Fields collection [ADOX]
ms.assetid: d8304849-3f80-4cf3-9425-529d2a8ebedd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5cbf00fc32364c1077be44ebb791708f361ec4da
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768984"
---
# <a name="views-and-fields-collections-example-vb"></a>Ejemplo de colecciones de vistas y campos (VB)
En el código siguiente se muestra cómo utilizar la propiedad de [comando](./command-property-adox.md) y el objeto de [conjunto de registros](../ado-api/recordset-object-ado.md) para recuperar la información de campo de la vista.  
  
```  
' BeginViewFieldsVB  
Sub ViewFields()  
    On Error GoTo ViewFieldsError  
  
    Dim cnn As New ADODB.Connection  
    Dim rst As New ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Set the Source for the Recordset  
    Set rst.Source = cat.Views("AllCustomers").Command  
  
    ' Retrieve Field information  
    rst.Fields.Refresh  
    For Each fld In rst.Fields  
        Debug.Print fld.Name & ":" & fld.Type  
    Next  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set rst = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ViewFieldsError:  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
  
    Set cat = Nothing  
    Set rst = Nothing  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndViewFieldsVB  
```  
  
## <a name="see-also"></a>Consulte también  
 [ActiveConnection (propiedad, ADOX)](./activeconnection-property-adox.md)   
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)   
 [Command (propiedad, ADOX)](./command-property-adox.md)   
 [Objeto de vista (ADOX)](./view-object-adox.md)   
 [Colección de vistas (ADOX)](./views-collection-adox.md)