---
title: Con un objeto de conexión | Documentos de Microsoft
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
- connections [ADO]
ms.assetid: 4b34f971-5699-43e7-9b15-137d334fa66e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7aa8e57d79b7f65ede84c7e88f03d18a5131f449
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="using-a-connection-object"></a>Uso de un objeto de conexión
Antes de abrir un **conexión** objeto, debe definir cierta información sobre el origen de datos y el tipo de conexión. La mayor parte de esta información se mantiene en el *ConnectionString* parámetro de la [Open (método)](../../../ado/reference/ado-api/open-method-ado-connection.md) en el **conexión** objeto, o por el [ConnectionString propiedad](../../../ado/reference/ado-api/connectionstring-property-ado.md) en el **conexión** objeto. Una cadena de conexión consta de una lista de pares de argumento y valor separados por punto y coma, con los valores encerrados entre comillas simples. Por ejemplo:  
  
```  
Dim sConn As String  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
```  
  
> [!NOTE]
>  También puede especificar un nombre de origen de datos ODBC (DSN) o un archivo de Data Link (UDL) en una cadena de conexión. Para obtener más información acerca de los DSN, vea [administrar orígenes de datos](../../../odbc/admin/managing-data-sources.md) en referencia del programador de ODBC. Para obtener más información acerca de los UDL, vea [información general sobre la API de vínculos de datos](http://msdn.microsoft.com/en-us/95c180ea-bd4f-4dca-b95a-576afd135bbc) en referencia de la base de datos del programador de OLE.  
  
 Por lo general, establecer una conexión mediante una llamada a la **Connection.Open** método con un adecuado un *cadena de conexión* como su parámetro. En el siguiente fragmento de código de Visual Basic, se muestra un ejemplo:  
  
```  
Dim oConn As ADODB.Connection  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
' Open a connection.  
Set oConn = New ADODB.Connection  
.Open   
  
' Make a query over the connection.  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
Set oRs = New ADODB.Recordset  
oRs.Open sSQL, , adOpenStatic, adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
' Close the connection.  
oConn.Close  
Set oConn = Nothing  
  
```  
  
 Aquí **oRs.Open** toma una **conexión** objeto (*oConn*) variable como el valor de su *ActiveConnection* parámetro. Además, el **Connection.CursorLocation** propiedad asume el valor predeterminado de **adUseServer**. Compare esta opción para la [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) ejemplo en la sección anterior. La siguiente instrucción daría como resultado errores en tiempo de ejecución.  
  
```  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
```
