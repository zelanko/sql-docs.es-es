---
title: Ejemplo de métodos GetPermissions y SetPermissions (VB) | Microsoft Docs
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
- SetPermissions method [ADOX], Visual Basic example
- GetPermissions method [ADOX], Visual Basic example
ms.assetid: aa366d98-8c7a-4189-bdd8-1d663b243d33
author: rothja
ms.author: jroth
ms.openlocfilehash: f87e7f9b32c123cae2918f89b92ac2928bb65c65
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764899"
---
# <a name="getpermissions-and-setpermissions-methods-example-vb"></a>Ejemplo de métodos GetPermissions y SetPermissions (VB)
En este ejemplo se muestran los métodos [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) y [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) . El código siguiente proporciona acceso completo para la tabla Orders al usuario administrador.  
  
```  
' BeginGrantPermissionsVB  
Sub GrantPermissions()  
    On Error GoTo GrantPermissionsError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim lngPerm As Long  
  
    ' Opens a connection to the northwind database  
    ' using the Microsoft Jet 4.0 provider  
    cnn.Provider = "Microsoft.Jet.OLEDB.4.0"  
    cnn.Open "Data Source='Northwind.mdb';" & _  
        "jet oledb:system database=" & _  
        "'system.mdw'"  
  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve original permissions  
    lngPerm = cat.Users("admin").GetPermissions("Orders", adPermObjTable)  
    Debug.Print "Original permissions: " & Str(lngPerm)  
  
    ' Revoke all permissions  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessRevoke, adRightFull  
  
    ' Display permissions  
    Debug.Print "Revoked permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    ' Give the Admin user full rights on the orders object  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessSet, adRightFull  
  
    ' Display permissions  
    Debug.Print "Full permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    ' Restore original permissions  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessSet, lngPerm  
  
    ' Display permissions  
    Debug.Print "Final permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
GrantPermissionsError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndGrantPermissionsVB  
```  
  
## <a name="see-also"></a>Consulte también  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [GetPermissions (método) (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [SetPermissions (método) (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)   
 [Objeto user (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)   
 [Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
