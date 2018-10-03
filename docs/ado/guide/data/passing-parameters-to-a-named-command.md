---
title: Pasar parámetros a un comando con nombre | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f7db54ca3cd3b7574896bac11bce87446b6d4b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773393"
---
# <a name="passing-parameters-to-a-named-command"></a>Pasar parámetros a un comando con nombre
Al igual que el resultado del comando se pasa como un *out* variable del comando con nombre, parámetros sido para un comando con parámetros puede pasado como *en* variables para el comando con nombre.  
  
 El siguiente código en el ejemplo se intenta recuperar todos los pedidos realizados por el cliente cuya **CustomerID** es "ALKFI" de la base de datos Northwind. El valor de **CustomerID** se proporciona en el momento cuando se llama el comando con nombre.  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 Tenga en cuenta que todos los parámetros de entrada deben preceder a cualquier variable de salida y los tipos de datos de parámetros deben coincidir o se pueden convertir a los de los campos correspondientes. La siguiente instrucción:  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 : se producirá un error de tipos de datos no coincidentes, porque el parámetro de entrada necesario es de un **cadena** tipo, no de un **entero** tipo.  
  
 La siguiente llamada:  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 : es válido, pero dará como resultado un conjunto porque ningún registro de este tipo existe en la base de datos de resultados vacío.  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
