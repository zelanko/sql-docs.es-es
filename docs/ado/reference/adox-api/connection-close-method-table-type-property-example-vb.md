---
description: Ejemplo de propiedad Type de tabla, método connection close (VB)
title: Ejemplo de propiedad de tipo de tabla método de cierre de conexión (VB) | Microsoft Docs
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
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b651389b4badd57e6a76b3b38c47c34cc814706
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770914"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Ejemplo de propiedad Type de tabla, método connection close (VB)
Si se establece la propiedad [ActiveConnection](./activeconnection-property-adox.md) en **Nothing** , se debe cerrar la conexión con el catálogo. Las colecciones asociadas estarán vacías. Todos los objetos que se crearon a partir de objetos de esquema en el catálogo se quedarán huérfanos. Todas las propiedades de los objetos que se han almacenado en caché seguirán estando disponibles, pero se producirá un error al intentar leer las propiedades que requieren una llamada al proveedor.  
  
```  
' BeginCloseConnectionVB  
Sub Main()  
    On Error GoTo CloseConnectionByNothingError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Set tbl = cat.Tables(0)  
    Debug.Print tbl.Type    ' Cache tbl.Type info  
    Set cat.ActiveConnection = Nothing  
    Debug.Print tbl.Type    ' tbl is orphaned  
    ' Previous line will succeed if this info was cached.  
    Debug.Print tbl.Columns(0).DefinedSize  
    ' Previous line will fail if this info has not been cached.  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CloseConnectionByNothingError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCloseConnectionVB  
```  
  
 Cerrar un objeto de [conexión](../ado-api/connection-object-ado.md) que se usó para abrir el catálogo debería tener el mismo efecto que establecer la propiedad **ActiveConnection** en **Nothing**.  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>Consulte también  
 [ActiveConnection (propiedad, ADOX)](./activeconnection-property-adox.md)   
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)   
 [Objeto column (ADOX)](./column-object-adox.md)   
 [Colección de columnas (ADOX)](./columns-collection-adox.md)   
 [Objeto Table (ADOX)](./table-object-adox.md)   
 [Colección de tablas (ADOX)](./tables-collection-adox.md)   
 [Type (propiedad, tabla, ADOX)](./type-property-table-adox.md)