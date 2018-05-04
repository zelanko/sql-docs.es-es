---
title: Procedimientos de actualización de ejemplo del método (VB) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
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
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ad5229cc50c58b49e22d6a88808fc14c23703d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="procedures-refresh-method-example-vb"></a>Procedimientos de actualización de ejemplo del método (VB)
El código siguiente muestra cómo actualizar la [procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md) colección de un [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md). Esto es necesario antes de [procedimiento](../../../ado/reference/adox-api/procedure-object-adox.md) objetos desde la **catálogo** son accesibles.  
  
```  
' BeginProceduresRefreshVB  
Sub Main()  
    On Error GoTo ProcedureRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection  
    cat.Procedures.Refresh  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureRefreshError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProceduresRefreshVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
