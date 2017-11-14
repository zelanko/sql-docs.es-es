---
title: "Guardar y abrir un ejemplo de los métodos (VB) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad4d79342ae4903e3469f3685210e882d64d318f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="save-and-open-methods-example-vb"></a>Guardar y abrir un ejemplo de los métodos (VB)
Estos tres ejemplos se muestra cómo el [guardar](../../../ado/reference/ado-api/save-method.md) y [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) métodos se pueden usar conjuntamente.  
  
 Se supone que va en un viaje de negocios y desea trasladar a lo largo de una tabla de una base de datos. Antes de ir, tener acceso a los datos como un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) y guárdelo en un formato transportable. Cuando llega a su destino, tener acceso a la **Recordset** como un valor local desconectado **conjunto de registros**. Realizar cambios en el **Recordset**y, a continuación, vuelva a guardar. Por último, al volver a casa, conectarse de nuevo a la base de datos y actualizar con los cambios realizados en la carretera.  
  
 En primer lugar, obtenga acceso y guarde la ***autores*** tabla.  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 En este momento, ha llegado a su destino. Tendrá acceso a la ***autores*** tabla como un valor local desconectado **conjunto de registros**. Debe tener la **MSPersist** proveedor en el equipo que está utilizando para tener acceso al archivo guardado, a:\Pubs.xml.  
  
```  
Attribute VB_Name = "Save"  
```  
  
 Por último, vuelve a casa. Ahora puede actualizar la base de datos con los cambios.  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>Vea también  
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Más información acerca de la persistencia de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save (método)](../../../ado/reference/ado-api/save-method.md)

