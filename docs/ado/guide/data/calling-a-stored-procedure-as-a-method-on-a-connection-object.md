---
title: Llamar a un procedimiento almacenado como un método en un objeto de conexión | Microsoft Docs
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
ms.assetid: 35ffdb79-a931-4271-a3bb-0cd804cf173e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2189bf9b2a82cdf21fdd13ed77a977f6b333ac87
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925897"
---
# <a name="calling-a-stored-procedure-as-a-method-on-a-connection-object"></a>Llamar a un procedimiento almacenado como un método en un objeto de conexión
Puede llamar a un procedimiento almacenado como si fuera un método nativo en el objeto de **conexión** abierta asociado. Esto es similar a llamar a un comando con nombre en el objeto de **conexión** .  
  
 En el siguiente ejemplo de código de Visual Basic se llama a un procedimiento almacenado de la base de datos de ejemplo Northwind, denominado CustOrdersOrders, que se muestra aquí de nuevo para su comodidad.  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 En el ejemplo de código siguiente se muestra cómo llamar a un procedimiento almacenado como si fuera un método nativo en un objeto de **conexión** abierto asociado.  
  
```  
Const DS = "MySQLServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a stored procedure  
  
Set objComm.ActiveConnection = objConn  
  
' Execute the stored procedure on  
' the active connection object...  
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
  
' Display the result.  
Debug.Print "Results returned from sp_CustOrdersOrders for ALFKI: "  
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
Set objComm = Nothing  
```  
  
## <a name="see-also"></a>Consulte también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
