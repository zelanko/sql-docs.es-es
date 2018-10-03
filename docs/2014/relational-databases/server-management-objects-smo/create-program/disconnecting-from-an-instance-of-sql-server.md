---
title: Desconectar de una instancia de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: def5d709389f5d941678771ba41d7f41a00b7971
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48064925"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectar de una instancia de SQL Server
  Cerrar ni desconectar manualmente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] objetos Management Objects (SMO) no es necesario. Las conexiones se abren y se cierra según se requiere.  
  
## <a name="connection-pooling"></a>Agrupar conexiones  
 Cuando el <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> se llama al método, la conexión no se libera automáticamente. Para liberar la conexión al grupo de conexiones, se debe llamar al método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> explícitamente. También puede solicitar una conexión no agrupada. Para ello, establezca la propiedad <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> de la propiedad <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> que hace referencia al objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectar de una instancia de SQL Server para RMO  
 El cierre de las conexiones de servidor cuando se programa con RMO funciona de forma ligeramente diferente a SMO.  
  
 Dado que la conexión del servidor para un objeto RMO se mantiene por el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto, este objeto también se utiliza al desconectar de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando se programa mediante el uso de RMO. Para cerrar una conexión con el <xref:Microsoft.SqlServer.Management.Common.ServerConnection> de objeto, llame a la <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> método del objeto RMO. Una vez cerrada la conexión, no se pueden utilizar objetos RMO.  
  
## <a name="example"></a>Ejemplo  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Cerrar y desconectar un objeto SMO en Visual Basic  
 Este ejemplo de código muestra cómo solicitar una conexión no agrupada estableciendo la <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad de objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Cerrar y desconectar un objeto SMO en Visual C#  
 Este ejemplo de código muestra cómo solicitar una conexión no agrupada estableciendo la <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad de objeto.  
  
```  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
