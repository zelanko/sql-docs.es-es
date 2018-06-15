---
title: Catálogo de ejemplo de propiedad ActiveConnection (VB) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 078d5bad66b0f50f0baae63b0c0aeab8313207c7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285234"
---
# <a name="catalog-activeconnection-property-example-vb"></a>Ejemplo de propiedad ActiveConnection de catálogo (VB)
Establecer el [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propiedad a una conexión abierta válida, "abre" el catálogo. Desde un catálogo abierto, puede tener acceso a los objetos de esquema dentro de dicho catálogo.  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 Establecer el **ActiveConnection** propiedad en una cadena de conexión válida también "abre" el catálogo.  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection (propiedad, ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Objeto de tabla (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type (propiedad, tabla, ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
