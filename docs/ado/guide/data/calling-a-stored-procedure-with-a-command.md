---
title: Llamar a un procedimiento almacenado con un comando | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35c1fce22e700ddd7ca2e738449a7b8b4ce4a63a
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51601476"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Llamar a un procedimiento almacenado con un comando
Puede utilizar un comando para llamar a un procedimiento almacenado. El ejemplo de código al final de este tema hace referencia a un procedimiento almacenado en la base de datos de ejemplo Northwind, denominado CustOrdersOrders, que se define como sigue.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 Consulte la documentación de SQL Server para obtener más información acerca de cómo definir y llamar a procedimientos almacenados.  
  
 Este procedimiento almacenado es similar al comando utilizado en [parámetros del objeto Command](../../../ado/guide/data/command-object-parameters.md). Toma un parámetro de Id. cliente y devuelve información acerca de los pedidos del cliente. Ejemplo de código siguiente utiliza este procedimiento almacenado como el origen de ADO **Recordset**.  
  
 Mediante el procedimiento almacenado le permite tener acceso a otra funcionalidad de ADO: el **parámetros** colección **actualizar** método. Con este método, ADO puede rellenar automáticamente toda la información acerca de los parámetros requeridos por el comando en tiempo de ejecución. Hay una reducción del rendimiento en mediante esta técnica, ya que ADO debe consultar el origen de datos para obtener información sobre los parámetros.  
  
 Existen otras diferencias importantes entre el siguiente ejemplo de código y el código en [parámetros del objeto Command](../../../ado/guide/data/command-object-parameters.md), donde se especifican los parámetros manualmente. En primer lugar, este código no establece la **Prepared** propiedad **True** porque es un procedimiento almacenado de SQL Server y está precompilado por definición. Segundo, el **CommandType** propiedad de la **comando** objeto cambiado a **adCmdStoredProc** en el segundo ejemplo para informar a ADO que el comando era un procedimiento almacenado.  
  
 Por último, en el segundo ejemplo el parámetro se debe hacer referencia al índice al establecer el valor, porque no es posible que conoce el nombre del parámetro en tiempo de diseño. Si conoce el nombre del parámetro, puede establecer la nueva [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md) propiedad de la **comando** objeto en True y hacer referencia al nombre de la propiedad. Tal vez se pregunte por qué se ha mencionado en la posición del primer parámetro del procedimiento almacenado (@CustomerID) es 1 en lugar de 0 (`objCmd(1) = "ALFKI"`). Esto es porque el parámetro 0 contiene un valor devuelto por el procedimiento almacenado de SQL Server.  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
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
    Set objParm1 = Nothing  
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
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndAutoParamCmd  
  
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
  
## <a name="see-also"></a>Vea también  
 [Artículo de Knowledge Base 117500](https://go.microsoft.com/fwlink/?LinkId=117500)
