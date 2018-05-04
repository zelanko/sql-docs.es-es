---
title: Implementar extremos | Documentos de Microsoft
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
- endpoints [SMO]
ms.assetid: f8674dbb-9bc0-488f-9def-e9e0ce1ddf86
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3bca7603f7cc7d035b2fdf294694609e7b0a90c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="implementing-endpoints"></a>Implementar extremos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Un extremo es un servicio que puede escuchar originalmente las solicitudes. SMO es compatible con varios tipos de extremos utilizando el <xref:Microsoft.SqlServer.Management.Smo.Endpoint> objeto. Puede crear un servicio de extremos que administre un tipo específico de carga útil, que utiliza un protocolo concreto, creando una instancia de un objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint> y estableciendo sus propiedades.  
  
 El <xref:Microsoft.SqlServer.Management.Smo.Endpoint.EndpointType%2A> propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Endpoint> objeto puede utilizarse para especificar los siguientes tipos de carga:  
  
-   Creación de reflejo de base de datos  
  
-   SOAP (la compatibilidad con los extremos SOAP se encuentra en [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] y versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)])  
  
-   Service Broker  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
  
 Asimismo, la propiedad <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A> puede utilizarse para especificar los dos protocolos admitidos siguientes:  
  
-   Protocolo HTTP  
  
-   Protocolo TCP  
  
 Si ha especificado el tipo de carga, la carga real puede establecerse mediante el <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Payload%2A> propiedad de objeto. La propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.Payload> proporciona una referencia a un objeto de carga útil del tipo especificado, para el que se pueden modificar las propiedades.  
  
 Para el objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseMirroringPayload>, debe especificar el rol de creación de reflejo y si el cifrado está habilitado. La <xref:Microsoft.SqlServer.Management.Smo.ServiceBrokerPayload> objeto requiere información sobre el reenvío de mensajes, el número máximo de conexiones permitido y el modo de autenticación. El objeto <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethod.%23ctor%2A> exige establecer varias propiedades incluida la propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethodCollection.Add%2A>, que especifica los métodos de carga útil de SOAP disponibles para los clientes (procedimientos almacenados y funciones definidas por el usuario).  
  
 De igual forma, el protocolo actual se puede establecer utilizando la propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Protocol%2A> que hace referencia a un objeto de protocolo del tipo especificado por propiedad <xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A>. El objeto <xref:Microsoft.SqlServer.Management.Smo.HttpProtocol> requiere una lista de direcciones IP restringidas y la información sobre el puerto, sitio web y autenticación. La <xref:Microsoft.SqlServer.Management.Smo.TcpProtocol> objeto también requiere una lista de direcciones IP restringidas e información del puerto.  
  
 Si se ha creado el extremo y se ha definido totalmente, se puede conceder, revocar y denegar el acceso a los usuarios de la base de datos, grupos, roles e inicio de sesión.  
  
## <a name="example"></a>Ejemplo  
 Para el siguiente ejemplo de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, consulte [crear a Visual C&#35; proyecto SMO en Visual Studio .NET](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-basic"></a>Crear un servicio de extremo de creación de reflejo de base de datos en Visual Basic  
 En el ejemplo de código se muestra cómo crear un extremo de creación de reflejo de base de datos en SMO. Esto es necesario antes de crear un espejo de la base de datos. Utilice <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> y otras propiedades en el objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para crear un espejo de la base de datos.  
  
```VBNET
'Set up a database mirroring endpoint on the server before setting up a database mirror.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Endpoint object variable for database mirroring.
Dim ep As Endpoint
ep = New Endpoint(srv, "Mirroring_Endpoint")
ep.ProtocolType = ProtocolType.Tcp
ep.EndpointType = EndpointType.DatabaseMirroring
'Specify the protocol ports.
ep.Protocol.Http.SslPort = 5024
ep.Protocol.Tcp.ListenerPort = 6666
'Specify the role of the payload.
ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All
'Create the endpoint on the instance of SQL Server.
ep.Create()
'Start the endpoint.
ep.Start()
Console.WriteLine(ep.EndpointState)
``` 
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-c"></a>Crear un servicio de extremo de creación de reflejo de base de datos en Visual C#  
 En el ejemplo de código se muestra cómo crear un extremo de creación de reflejo de base de datos en SMO. Esto es necesario antes de crear un espejo de la base de datos. Utilice <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> y otras propiedades en el objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para crear un espejo de la base de datos.  
  
```csharp  
{  
            //Set up a database mirroring endpoint on the server before   
        //setting up a database mirror.   
        //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Define an Endpoint object variable for database mirroring.   
            Endpoint ep = default(Endpoint);  
            ep = new Endpoint(srv, "Mirroring_Endpoint");  
            ep.ProtocolType = ProtocolType.Tcp;  
            ep.EndpointType = EndpointType.DatabaseMirroring;  
            //Specify the protocol ports.   
            ep.Protocol.Http.SslPort = 5024;  
            ep.Protocol.Tcp.ListenerPort = 6666;  
            //Specify the role of the payload.   
            ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All;  
            //Create the endpoint on the instance of SQL Server.   
            ep.Create();  
            //Start the endpoint.   
            ep.Start();  
            Console.WriteLine(ep.EndpointState);  
        }  
```  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-powershell"></a>Crear un servicio de extremo de creación de reflejo de la base de datos en PowerShell  
 En el ejemplo de código se muestra cómo crear un extremo de creación de reflejo de base de datos en SMO. Esto es necesario antes de crear un espejo de la base de datos. Utilice <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> y otras propiedades en el objeto <xref:Microsoft.SqlServer.Management.Smo.Database> para crear un espejo de la base de datos.  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get a new endpoint to congure and add  
$ep = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Endpoint -argumentlist $srv,"Mirroring_Endpoint"  
  
#Set some properties  
$ep.ProtocolType = [Microsoft.SqlServer.Management.SMO.ProtocolType]::Tcp  
$ep.EndpointType = [Microsoft.SqlServer.Management.SMO.EndpointType]::DatabaseMirroring  
$ep.Protocol.Http.SslPort = 5024  
$ep.Protocol.Tcp.ListenerPort = 6666 #inline comment  
$ep.Payload.DatabaseMirroring.ServerMirroringRole = [Microsoft.SqlServer.Management.SMO.ServerMirroringRole]::All  
  
# Create the endpoint on the instance  
$ep.Create()  
  
# Start the endpoint  
$ep.Start()  
  
# Report its state  
$ep.EndpointState;  
```  
  
## <a name="see-also"></a>Vea también  
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
