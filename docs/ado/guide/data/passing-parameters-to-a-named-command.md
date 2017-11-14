---
title: "Pasar parámetros a un comando con nombre | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 33d1ee3fe4e24695deccd0615f17868bfdfd988c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="passing-parameters-to-a-named-command"></a>Pasar parámetros a un comando con nombre
Tal y como se pasa el resultado del comando como un *out* variable del comando con nombre, parámetros para un comando con parámetros puede sido pasado como *en* variables para el comando con nombre.  
  
 El siguiente código en el ejemplo se intenta recuperar todos los pedidos realizados por el cliente cuyo **CustomerID** es "ALKFI" de la base de datos Northwind. El valor de **CustomerID** se proporciona en el momento cuando se llama el comando indicado.  
  
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
  
 : es válido, pero dará un resultado vacío porque no existe ningún registro de este tipo en la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

