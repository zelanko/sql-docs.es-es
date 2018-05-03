---
title: Crear y ejecutar un comando Simple | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], creating and executing
- commands [ADO], creating and executing
ms.assetid: 0b81af6f-b9ae-4f7c-b59b-b5bdd775036f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 147ae6b84bb3b40b7737bf99ee427a73bff33eb6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="creating-and-executing-a-simple-command"></a>Crear y ejecutar un comando Simple
Un comando simple es uno que no tiene parámetros y no requiere ninguna persistencia. Hay tres maneras de crear y ejecutar un comando simple.  
  
-   Con un **comando** objeto  
  
-   Con un **conexión** objeto  
  
-   Con un **Recordset** objeto  
  
## <a name="using-a-command-object"></a>Uso de un objeto de comando  
 Para crear un comando simple mediante una **comando** objeto, debe asignar la instrucción en el **CommandText** propiedad de un **comando** de objeto y establecer el valor adecuado para el **CommandType** propiedad. Ejecutar el comando requiere que se asigna una conexión abierta a la **ActiveConnection** propiedad de la **comando** objeto, seguida de una llamada a la **Execute** (método) en el **comando** objeto.  
  
 El fragmento de código siguiente muestra el método básico del uso de la **comando** objeto que se va a ejecutar un comando en un origen de datos. Este ejemplo utiliza un comando que devuelve filas y devuelve los resultados de la ejecución del comando como un **Recordset** objeto.  
  
```  
    'BeginBasicCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objRs As New ADODB.Recordset  
  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = 'ALFKI' " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print "ALFKI"  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndBasicCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
## <a name="using-a-recordset-object"></a>Mediante un objeto de conjunto de registros  
 También puede crear un comando como una cadena de texto y PA a la **abiertos** método en un **Recordset** objeto, junto con el tipo de comando (adCmdText), para la ejecución. Esto se muestra en el siguiente fragmento de código.  
  
```  
  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objRs As New ADODB.Recordset  
Dim CommandText As String  
Dim ConnctionString As String  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to data source and execute the SQL command.  
objRs.Open CommandText, ConnectionString, _  
            adOpenStatic, adLockReadOnly, adCmdText  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
Set objRs = Nothing  
```  
  
## <a name="using-a-connection-object"></a>Uso de un objeto de conexión  
 También puede ejecutar un comando en un objeto de conexión abierto. El ejemplo de código anterior se convertirá en esto:  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = 'ALFKI' " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Execute command through the connection and display...  
Set objRs = objConn.Execute(CommandText)  
  
Debug.Print "ALFKI"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```
