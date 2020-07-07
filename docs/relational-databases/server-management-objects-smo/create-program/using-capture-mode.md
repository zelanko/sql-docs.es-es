---
title: Usar el modo de captura | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0e2a743ce34df434e9324a973208f18475ad1ae7
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008660"
---
# <a name="using-capture-mode"></a>Utilizar el modo de captura
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Los programas SMO capturan y graban las instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)] equivalentes emitidas por el programa en lugar de, o además de, las instrucciones que son ejecutadas por el programa. Puede habilitar el modo de captura utilizando el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> o utilizando la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
## <a name="example"></a>Ejemplo  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  

  
## <a name="enabling-capture-mode-in-visual-basic"></a>Habilitar el modo de captura en Visual Basic  
 En este ejemplo de código se habilita el modo de captura y, a continuación, se muestran los comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contenidos en el búfer de captura.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Set the execution mode to CaptureSql for the connection.
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql
'Make a modification to the server that is to be captured.
srv.UserOptions.AnsiNulls = True
srv.Alter()
'Iterate through the strings in the capture buffer and display the captured statements.
Dim s As String
For Each s In srv.ConnectionContext.CapturedSql.Text
    Console.WriteLine(s)
Next
'Execute the captured statements.
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text)
'Revert to immediate execution mode. 
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql
```
  
## <a name="enabling-capture-mode-in-visual-c"></a>Habilitar el modo de captura en Visual C#  
 En este ejemplo de código se habilita el modo de captura y, a continuación, se muestran los comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contenidos en el búfer de captura.  
  
```csharp  
{   
// Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
// Set the execution mode to CaptureSql for the connection.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.CaptureSql;   
// Make a modification to the server that is to be captured.   
srv.UserOptions.AnsiNulls = true;   
srv.Alter();   
// Iterate through the strings in the capture buffer and display the captured statements.   
string s;   
foreach ( String p_s in srv.ConnectionContext.CapturedSql.Text ) {   
   Console.WriteLine(p_s);   
}   
// Execute the captured statements.   
srv.ConnectionContext.ExecuteNonQuery(srv.ConnectionContext.CapturedSql.Text);   
// Revert to immediate execution mode.   
srv.ConnectionContext.SqlExecutionModes = SqlExecutionModes.ExecuteSql;   
}  
```  
  
  
