---
title: Ejemplo de la propiedad ActiveCommand (VB) | Microsoft Docs
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
- ActiveCommand property [ADO], Visual Basic example
ms.assetid: 23b06499-62df-4f46-88eb-6da392f9b456
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d97f655c89c07f7866fbdee6aab236f942b5499c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921686"
---
# <a name="activecommand-property-example-vb"></a>Ejemplo de la propiedad ActiveCommand (VB)
En este ejemplo se muestra la propiedad [ActiveCommand](../../../ado/reference/ado-api/activecommand-property-ado.md) .  
  
 A una subrutina se le asigna un objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) cuya propiedad **ActiveCommand** se usa para mostrar el texto del comando y el parámetro que creó el **conjunto de registros**.  
  
```  
'BeginActiveCommandVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
        'recordset and connection variables  
    Dim cmd As ADODB.Command  
    Dim rst As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
        'record variables  
    Dim strPrompt As String  
    Dim strName As String  
  
    Set Cnxn = New ADODB.Connection  
    Set cmd = New ADODB.Command  
  
    strPrompt = "Enter an author's name (e.g., Ringer): "  
    strName = Trim(InputBox(strPrompt, "ActiveCommandX Example"))  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
        'create SQL command string  
    cmd.CommandText = "SELECT * FROM Authors WHERE au_lname = ?"  
    cmd.Parameters.Append cmd.CreateParameter("LastName", adChar, adParamInput, 20, strName)  
  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
  
        'create the recordset by executing command string  
    Set rst = cmd.Execute(, , adCmdText)  
        'see the results  
    Call ActiveCommandXprint(rst)  
  
    ' clean up  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndActiveCommandVB  
```  
  
 La rutina **ActiveCommandXprint** solo recibe un objeto de **conjunto de registros** , pero debe imprimir el texto del comando y el parámetro que creó el conjunto de **registros**. Esto se puede hacer porque la propiedad **ActiveCommand** del objeto de **conjunto de registros** produce el objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) asociado.  
  
 La propiedad [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) del objeto de **comando** produce el comando con parámetros que creó el **conjunto de registros**. La colección de [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) del objeto **Command** produce el valor que se sustituyó por el marcador de posición de parámetro del comando ("**?**").  
  
 Por último, se imprimen un mensaje de error o el nombre e identificador del autor.  
  
```  
'BeginActiveCommandPrintVB  
Public Sub ActiveCommandXprint(rstp As ADODB.Recordset)  
  
    Dim strName As String  
  
    strName = rstp.ActiveCommand.Parameters.Item("LastName").Value  
  
    Debug.Print "Command text = '"; rstp.ActiveCommand.CommandText; "'"  
    Debug.Print "Parameter = '"; strName; "'"  
  
    If rstp.BOF = True Then  
       Debug.Print "Name = '"; strName; "', not found."  
    Else  
       Debug.Print "Name = '"; rstp!au_fname; " "; rstp!au_lname; _  
             "', author ID = '"; rstp!au_id; "'"  
    End If  
  
    rstp.Close  
    Set rstp = Nothing  
End Sub  
'EndActiveCommandPrintVB  
```  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad ActiveCommand (ADO)](../../../ado/reference/ado-api/activecommand-property-ado.md)   
 [Command (objeto) (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
