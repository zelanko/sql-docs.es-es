---
title: Ejemplo de las propiedades Provider y DefaultDatabase (VB) | Microsoft Docs
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
- DefaultDatabase property [ADO], Visual Basic example
- provider property [ADO], Visual Basic example
ms.assetid: 677e1dbe-bcf6-4028-a62c-e99b1c88bf7b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46486167ab5e8bd1b063928d4ba3f6f73c893784
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931513"
---
# <a name="provider-and-defaultdatabase-properties-example-vb"></a>Ejemplo de las propiedades Provider y DefaultDatabase (VB)
En este ejemplo se muestra la propiedad de [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) abriendo tres objetos de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) mediante proveedores diferentes. También utiliza la propiedad [DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md) para establecer la base de datos predeterminada para el proveedor ODBC de Microsoft.  
  
> [!NOTE]
>  Si se va a conectar a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = Yes** o **Integrated Security = SSPI** en lugar de la información de identificador de usuario y contraseña en la cadena de conexión.  
  
```  
'BeginProviderVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection strings  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn1 As ADODB.Connection  
    Dim Cnxn2 As ADODB.Connection  
    Dim Cnxn3 As ADODB.Connection  
    Dim strCnxn As String  
  
    ' Open a connection using the Microsoft ODBC provider  
    Set Cnxn1 = New ADODB.Connection  
    Cnxn1.ConnectionString = "driver={SQL Server};server='MySqlServer';" & _  
        "user id='MyUserID';password='MyPassword';"  
    Cnxn1.Open strCnxn  
    Cnxn1.DefaultDatabase = "Pubs"  
  
    ' Display the provider  
    MsgBox "Cnxn1 provider: " & Cnxn1.Provider  
  
    ' Open a connection using the Microsoft Jet provider  
    Set Cnxn2 = New ADODB.Connection  
    Cnxn2.Provider = "Microsoft.Jet.OLEDB.4.0"  
    Cnxn2.Open "Northwind.mdb", _  
        "MyUserID", "MyPassword"  
  
    ' Display the provider.  
    MsgBox "Cnxn2 provider: " & Cnxn2.Provider  
  
    ' Open a connection using the Microsoft SQL Server provider  
    Set Cnxn3 = New ADODB.Connection  
    Cnxn3.Provider = "sqloledb"  
    Cnxn3.Open "Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    ' Display the provider  
    MsgBox "Cnxn3 provider: " & Cnxn3.Provider  
  
    ' clean up  
    Cnxn1.Close  
    Cnxn2.Close  
    Cnxn3.Close  
    Set Cnxn1 = Nothing  
    Set Cnxn2 = Nothing  
    Set Cnxn3 = Nothing  
    Exit Sub  
  
ErrorHandler:  
    If Not Cnxn1 Is Nothing Then  
        If Cnxn1.State = adStateOpen Then Cnxn1.Close  
    End If  
    Set Cnxn1 = Nothing  
  
    If Not Cnxn2 Is Nothing Then  
        If Cnxn2.State = adStateOpen Then Cnxn2.Close  
    End If  
    Set Cnxn2 = Nothing  
  
    If Not Cnxn3 Is Nothing Then  
        If Cnxn3.State = adStateOpen Then Cnxn3.Close  
    End If  
    Set Cnxn3 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndProviderVB  
```  
  
## <a name="see-also"></a>Consulte también  
 [Connection (objeto) (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Propiedad DefaultDatabase](../../../ado/reference/ado-api/defaultdatabase-property.md)   
 [Propiedad de proveedor (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)
