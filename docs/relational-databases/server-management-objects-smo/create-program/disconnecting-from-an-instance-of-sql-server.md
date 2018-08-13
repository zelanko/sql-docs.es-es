---
title: Desconectar de una instancia de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: fffcb2d7d9ef6f9d8b0f3e13717985f7a8032047
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555445"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>Desconectar de una instancia de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Cerrar ni desconectar manualmente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] objetos Management Objects (SMO) no es necesario. Las conexiones se abren y se cierra según se requiere.  
  
## <a name="connection-pooling"></a>Agrupar conexiones  
 Cuando el [Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect) se llama al método, la conexión no se libera automáticamente. El [desconexión](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) método se debe llamar explícitamente para liberar la conexión al grupo de conexiones. También puede solicitar una conexión no agrupada. Hacerlo estableciendo la [NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> propiedad que hace referencia el [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto.  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>Desconectar de una instancia de SQL Server para RMO  
 El cierre de las conexiones de servidor cuando se programa con RMO funciona de forma ligeramente diferente a SMO.  
  
 Dado que la conexión del servidor para un objeto RMO se mantiene por el [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) objeto, este objeto también se utiliza al desconectar de una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando se programa mediante el uso de RMO. Para cerrar una conexión con el [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx) de objeto, llame a la [desconexión](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect) método del objeto RMO. Una vez cerrada la conexión, no se pueden utilizar objetos RMO.  
  
## <a name="example"></a>Ejemplo  
Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
 
  
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
  
  
