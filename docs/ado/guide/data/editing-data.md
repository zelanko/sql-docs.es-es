---
title: "Edición de datos | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7048a7774e965f29d67ba1cbc65aac51dde1c271
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="editing-data"></a>Edición de datos
Ya se explicó cómo utilizar ADO para conectarse a un origen de datos, ejecutar un comando, obtener los resultados en un **Recordset** de objetos y navegar dentro de la **conjunto de registros**. En esta sección se centra en la siguiente operación fundamental de ADO: edición de datos.  
  
 En esta sección continúa usando el ejemplo **Recordset** introducidas en [examinar datos](../../../ado/guide/data/examining-data.md), con un cambio importante. El código siguiente se utiliza para abrir el **Recordset**:  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 El cambio importante en el código implica la configuración de la **CursorLocation** propiedad de la **conexión** igual al objeto **adUseClient** en el  *GetNewConnection* función (que se muestra en el ejemplo siguiente), que indica el uso de un cursor de cliente. Para obtener más información sobre las diferencias entre los cursores de cliente y servidor, consulte [cursores y bloqueos](../../../ado/guide/data/understanding-cursors-and-locks.md).  
  
 El **CursorLocation** la propiedad **adUseClient** mueve la ubicación del cursor desde el origen de datos (SQL Server en este caso) a la ubicación del código de cliente (la estación de trabajo de escritorio). Esta opción obliga a ADO a invocar el motor de Cursor de cliente para OLE DB en el cliente con el fin de crear y administrar el cursor.  
  
 Es posible que haya observado que el **LockType** parámetro de la **abiertos** método cambiado a **adLockBatchOptimistic**. El cursor se abre en modo por lotes. (El proveedor almacena varios cambios en caché y los escribe en el origen de datos subyacente sólo cuando se llama a la **UpdateBatch** método.) Cambios realizados en el **Recordset** no se actualizará en la base de datos hasta que la **UpdateBatch** se llama al método.  
  
 Por último, el código de esta sección utiliza una versión modificada de la función GetNewConnection. Esta versión de la función devuelve ahora un cursor de cliente. La función tiene el siguiente aspecto:  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 Esta sección contiene los temas siguientes.  
  
-   [Editar los registros existentes](../../../ado/guide/data/editing-existing-records.md)  
  
-   [Agregar registros a un conjunto de registros](../../../ado/guide/data/adding-records.md)  
  
-   [Determinar qué se admite](../../../ado/guide/data/determining-what-is-supported.md)  
  
-   [Eliminar registros mediante el método Delete](../../../ado/guide/data/deleting-records-using-the-delete-method.md)  
  
-   [Alternativas: Utilizar instrucciones SQL](../../../ado/guide/data/alternatives-using-sql-statements.md)
