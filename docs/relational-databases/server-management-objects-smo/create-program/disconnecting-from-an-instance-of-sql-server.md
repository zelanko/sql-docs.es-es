---
title: Desconectar de una instancia de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 123283dc68ed21ba4c35d620abf80ff85b4a469c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectar de una instancia de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  No se requiere cerrar ni desconectar manualmente los objetos de Objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO). Las conexiones se abren y se cierra según se requiere.  
  
## <a name="connection-pooling"></a>Agrupar conexiones  
 Cuando el [conectar](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect) se llama al método, la conexión no se libera automáticamente. El [desconexión](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) método se debe llamar explícitamente para liberar la conexión al grupo de conexiones. También puede solicitar una conexión no agrupada. Para ello, establezca la [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad que hace referencia el [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectar de una instancia de SQL Server para RMO  
 El cierre de las conexiones de servidor cuando se programa con RMO funciona de forma ligeramente diferente a SMO.  
  
 Dado que la conexión del servidor de un objeto RMO se mantiene por la [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto, este objeto también se utiliza al desconectar de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando se programan mediante RMO. Para cerrar una conexión con el [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto, llame a la [desconexión](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) método del objeto RMO. Una vez cerrada la conexión, no se pueden utilizar objetos RMO.  
  
## <a name="example"></a>Ejemplo  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, consulte [crear a Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Cerrar y desconectar un objeto SMO en Visual Basic  
 Este ejemplo de código muestra cómo solicitar una conexión no agrupada estableciendo la [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad de objeto.  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Cerrar y desconectar un objeto SMO en Visual C#  
 Este ejemplo de código muestra cómo solicitar una conexión no agrupada estableciendo la [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad de objeto.  
  
```csharp  
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
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
