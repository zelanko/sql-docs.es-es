---
title: "Vistas de actualización de ejemplo del método (VB) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords: Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5ea5fe2d354acab56c432a47698177acd9e418f4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="views-refresh-method-example-vb"></a>Vistas de actualización de ejemplo del método (VB)
El código siguiente muestra cómo actualizar la [vistas](../../../ado/reference/adox-api/views-collection-adox.md) colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Esto es necesario antes de [vista](../../../ado/reference/adox-api/view-object-adox.md) objetos desde la **catálogo** son accesibles.  
  
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
 [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
