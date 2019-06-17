---
title: BOF, EOF y Bookmark propiedades ejemplo (VB) | Microsoft Docs
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
- BOF property [ADO], Visual Basic example
- Bookmark property [ADO], Visual Basic example
- EOF property [ADO], Visual Basic example
ms.assetid: b6573c6e-fee8-4267-a722-fadaec6eafe6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0ccaa2b12229077d21cd50ce73d55ff287507f0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66696329"
---
# <a name="bof-eof-and-bookmark-properties-example-vb"></a>Ejemplo de las propiedades BOF, EOF y Bookmark (VB)
Este ejemplo se usa el [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) y [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedades para mostrar un mensaje si un usuario intenta pasar el primer o último registro de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Usa el [marcador](../../../ado/reference/ado-api/bookmark-property-ado.md) propiedad para permitir que el usuario marca un registro en un **Recordset** y volver a él más adelante.  
  
```  
'BeginBOFVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim rstPublishers As ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLPubs As String  
     'record variables  
    Dim strMessage As String  
    Dim intCommand As Integer  
    Dim varBookmark As Variant  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' Open recordset and use client cursor  
     ' to enable AbsolutePosition property  
    Set rstPublishers = New ADODB.Recordset  
    strSQLPubs = "SELECT pub_id, pub_name FROM publishers ORDER BY pub_name"  
    rstPublishers.Open strSQLPubs, strCnxn, adUseClient, adOpenStatic, adCmdText  
  
    rstPublishers.MoveFirst  
    Do Until rstPublishers.EOF  
        ' Display information about current record  
        ' and get user input  
        strMessage = "Publisher: " & rstPublishers!pub_name & _  
            vbCr & "(record " & rstPublishers.AbsolutePosition & _  
            " of " & rstPublishers.RecordCount & ")" & vbCr & vbCr & _  
            "Enter command:" & vbCr & _  
            "[1 - next / 2 - previous /" & vbCr & _  
            "3 - set bookmark / 4 - go to bookmark]"  
        intCommand = Val(InputBox(strMessage))  
  
        ' Check user input  
        Select Case intCommand  
            Case 1  
                ' Move forward trapping for EOF  
                rstPublishers.MoveNext  
                If rstPublishers.EOF Then  
                    MsgBox "Moving past the last record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveLast  
                End If  
            Case 2  
                ' Move backward trapping for BOF  
                rstPublishers.MovePrevious  
                If rstPublishers.BOF Then  
                    MsgBox "Moving past the first record." & _  
                        vbCr & "Try again."  
                    rstPublishers.MoveFirst  
                End If  
            Case 3  
                ' Store the bookmark of the current record  
                varBookmark = rstPublishers.Bookmark  
            Case 4  
                ' Go to the record indicated by the stored bookmark  
                If IsEmpty(varBookmark) Then  
                    MsgBox "No Bookmark set!"  
                Else  
                    rstPublishers.Bookmark = varBookmark  
                End If  
            Case Else  
                Exit Do  
        End Select  
    Loop  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndBOFVB  
```  
  
 Este ejemplo se usa el **marcador** y [filtro](../../../ado/reference/ado-api/filter-property.md) propiedades para crear una vista limitada de la **Recordset**. Solo los registros que se hace referencia a la matriz de los marcadores son accesibles.  
  
```  
Attribute VB_Name = "BOF"  
```  
  
## <a name="see-also"></a>Vea también  
 [BOF, EOF (propiedades) (ADO)](../../../ado/reference/ado-api/bof-eof-properties-ado.md)   
 [Bookmark (propiedad) (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
