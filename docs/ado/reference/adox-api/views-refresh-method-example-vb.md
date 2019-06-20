---
title: Vistas de actualización de ejemplo del método (VB) | Microsoft Docs
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
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a83ddfe567a0a4fc900e3098e0cb33b00e417c73
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697050"
---
# <a name="views-refresh-method-example-vb"></a>Ejemplo de método Refresh de vistas (VB)
El código siguiente muestra cómo actualizar el [vistas](../../../ado/reference/adox-api/views-collection-adox.md) colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Esto es necesario antes de [vista](../../../ado/reference/adox-api/view-object-adox.md) objetos desde el **catálogo** se puede tener acceso.  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Actualizar (método) (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
