---
title: Usar el modo de captura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, capture mode
- capture mode [SMO]
- SMO [SQL Server], capture mode
ms.assetid: ace29bf0-705a-434f-82e4-db99d01c5008
author: stevestein
ms.author: sstein
ms.openlocfilehash: 54c1cb71a3a5ed546c7408d3fcb747792e9cc248
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063104"
---
# <a name="using-capture-mode"></a>Utilizar el modo de captura
  Los programas SMO capturan y graban las instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)] equivalentes emitidas por el programa en lugar de, o además de, las instrucciones que son ejecutadas por el programa. Puede habilitar el modo de captura utilizando el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> o utilizando la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
## <a name="example"></a>Ejemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="enabling-capture-mode-in-visual-basic"></a>Habilitar el modo de captura en Visual Basic  
 En este ejemplo de código se habilita el modo de captura y, a continuación, se muestran los comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contenidos en el búfer de captura.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCapture1](SMO How to#SMO_VBCapture1)]  -->  
  
## <a name="enabling-capture-mode-in-visual-c"></a>Habilitar el modo de captura en Visual C#  
 En este ejemplo de código se habilita el modo de captura y, a continuación, se muestran los comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] contenidos en el búfer de captura.  
  
```  
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
  
  
