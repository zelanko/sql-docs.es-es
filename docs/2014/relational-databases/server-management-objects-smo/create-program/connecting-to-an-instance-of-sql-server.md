---
title: Conectarse a una instancia de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, connections
- connections [SMO]
- instances of SQL Server, connections
- SMO [SQL Server], connections
ms.assetid: ad3cf354-b2e3-468b-b986-1232e375fd84
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 88cb327d904d1c1fd79168f51c61ee122268667b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159955"
---
# <a name="connecting-to-an-instance-of-sql-server"></a>Conectarse a una instancia de SQL Server
  El primer paso de programación un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] application Management Objects (SMO) es crear una instancia de la <xref:Microsoft.SqlServer.Management.Smo.Server> objeto y establecer su conexión a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Puede crear una instancia del objeto <xref:Microsoft.SqlServer.Management.Smo.Server> y establecer una conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de tres maneras. La primera es utilizar una variable de objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para proporcionar la información de conexión. La segunda es proporcionar la información de conexión estableciendo explícitamente las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. La tercera es pasar el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el constructor del objeto <xref:Microsoft.SqlServer.Management.Smo.Server>.  
  
 **Uso de un objeto ServerConnection**  
  
 La ventaja de utilizar la variable de objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> es que se puede reutilizar la información de conexión. Declare una variable de objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. A continuación, declare un objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> y establezca las propiedades con información de conexión como el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el modo de autenticación. A continuación, pase la variable de objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> como parámetro al constructor de objeto <xref:Microsoft.SqlServer.Management.Smo.Server>. No se recomienda compartir a la vez las conexiones entre objetos de servidor distintos. Utilice el método <xref:Microsoft.SqlServer.Management.Common.ServerConnection.Copy%2A> para obtener una copia de los valores de conexión existentes.  
  
 **Establecer las propiedades del objeto Server explícitamente**  
  
 De modo alternativo, puede declarar la variable de objeto <xref:Microsoft.SqlServer.Management.Smo.Server> y llamar al constructor predeterminado. Tal cual, el objeto <xref:Microsoft.SqlServer.Management.Smo.Server> intenta conectarse a la instancia predeterminada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con todos los valores de conexión predeterminados.  
  
 **Proporcionar el nombre de instancia de SQL Server en el constructor del objeto de servidor**  
  
 Declare la variable de objeto <xref:Microsoft.SqlServer.Management.Smo.Server> y pase el nombre de instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como parámetro de cadena en el constructor. El objeto <xref:Microsoft.SqlServer.Management.Smo.Server> establece una conexión con la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con los valores de conexión predeterminados.  
  
## <a name="connection-pooling"></a>Agrupar conexiones  
 No se requiere normalmente llamar al método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> del objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. SMO establecerá automáticamente una conexión cuando sea necesario y liberará la conexión al grupo de conexiones después de haber terminado de realizar las operaciones. Cuando se llama al método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>, no se libera la conexión al grupo. Es necesaria una llamada explícita al método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> para liberar la conexión al grupo. Además, puede solicitar una conexión no agrupada estableciendo la propiedad <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> del objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
## <a name="multithreaded-applications"></a>Aplicaciones multiproceso  
 Para las aplicaciones multiproceso, se debe utilizar un objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> independiente en cada subproceso.  
  
## <a name="connecting-to-an-instance-of-sql-server-for-rmo"></a>Conectarse a una instancia de SQL Server para RMO  
 Replication Management Objects (RMO) usa un método ligeramente distinto de SMO para conectarse a un servidor de replicación.  
  
 Los objetos de programación RMO requieren que se realice una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> implementado por el espacio de nombres `Microsoft.SqlServer.Management.Common`. Esta conexión al servidor se realiza independientemente de los objetos de programación RMO. A continuación, se pasa al objeto RMO durante la creación de la instancia o por asignación a la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> del objeto. De esta manera, se pueden crear y administrar los objetos de programación RMO y las instancias de objeto de conexión por separado y se puede reutilizar un objeto de conexión único con varios objetos de programación RMO. Las reglas siguientes se aplican a las conexiones a un servidor de replicación:  
  
-   Todas las propiedades de la conexión se definen para un objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> especificado.  
  
-   Cada conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] debe tener su propio objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   Toda la información de autenticación para realizar la conexión e iniciar sesión en el servidor correctamente se proporciona en el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   De forma predeterminada, las conexiones se realizan mediante la autenticación de Microsoft Windows. Para utilizar la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> debe estar establecido en False y <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> y <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> deben estar establecidos en un inicio de sesión y contraseña de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válidos. Las credenciales de seguridad deben estar almacenadas y administradas de forma segura siempre y proporcionarse en tiempo de ejecución siempre que sea posible.  
  
-   Se debe llamar al método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> antes de pasar la conexión a cualquier objeto de programación RMO.  
  
## <a name="examples"></a>Ejemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Conectarse a la instancia local de SQL Server mediante la autenticación de Windows en Visual Basic  
 Para conectarse a la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se requiere mucho código. En su lugar, se basa en la configuración predeterminada del método de autenticación y servidor. La primera operación que exija la recuperación de datos hará que se cree una conexión.  
  
 En este ejemplo es [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] código .NET que se conecta a la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de Windows.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB1](SMO How to#SMO_VB1)]  -->  
  
## <a name="connecting-to-the-local-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Conectarse a la instancia local de SQL Server mediante la autenticación de Windows en Visual C#  
 Para conectarse a la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se requiere mucho código. En su lugar, se basa en la configuración predeterminada del método de autenticación y servidor. La primera operación que exija la recuperación de datos hará que se cree una conexión.  
  
 Este ejemplo está formado por código Visual C# .NET que se conecta a la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de Windows.  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//The connection is established when a property is requested.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-basic"></a>Conectarse a una instancia remota de SQL Server mediante la autenticación de Windows en Visual Basic  
 Al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de Windows, no es necesario especificar el tipo de autenticación. La autenticación de Windows es el valor predeterminado.  
  
 En este ejemplo es [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] código .NET que se conecta a la instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de Windows. La variable de cadena *strServer* contiene el nombre de la instancia remota.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB2](SMO How to#SMO_VB2)]  -->  
  
## <a name="connecting-to-a-remote-instance-of-sql-server-by-using-windows-authentication-in-visual-c"></a>Conectarse a una instancia remota de SQL Server mediante la autenticación de Windows en Visual C#  
 Al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de Windows, no es necesario especificar el tipo de autenticación. La autenticación de Windows es el valor predeterminado.  
  
 Este ejemplo está formado por código Visual C# .NET que se conecta a la instancia remota de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de Windows. La variable de cadena *strServer* contiene el nombre de la instancia remota.  
  
```  
{   
//Connect to a remote instance of SQL Server.   
Server srv;   
//The strServer string variable contains the name of a remote instance of SQL Server.   
srv = new Server(strServer);   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
}   
//The connection is automatically disconnected when the Server variable goes out of scope.  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-basic"></a>Conectarse a una instancia de SQL Server mediante la autenticación de SQL Server en Visual Basic  
 Al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], debe especificar el tipo de autenticación. En este ejemplo se muestra un método alternativo para declarar una variable de objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, que permite reutilizar la información de conexión.  
  
 El ejemplo es [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] código .NET que se muestra cómo conectarse a la instancia remota y *vPassword* contienen el inicio de sesión y la contraseña.  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll  
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim sqlServerLogin As [String] = "user_id"  
      Dim password As [String] = "pwd"  
      Dim instanceName As [String] = "instance_name"  
      Dim remoteSvrName As [String] = "remote_server_name"  
  
      ' Connecting to an instance of SQL Server using SQL Server Authentication  
      Dim srv1 As New Server()   ' connects to default instance  
      srv1.ConnectionContext.LoginSecure = False   ' set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin  
      srv1.ConnectionContext.Password = password  
      Console.WriteLine(srv1.Information.Version)   ' connection is established  
  
      ' Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      Dim srvConn As New ServerConnection()  
      srvConn.ServerInstance = ".\" & instanceName   ' connects to named instance  
      srvConn.LoginSecure = False   ' set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin  
      srvConn.Password = password  
      Dim srv2 As New Server(srvConn)  
      Console.WriteLine(srv2.Information.Version)   ' connection is established  
  
      ' For remote connection, remote server name / ServerInstance needs to be specified  
      Dim srvConn2 As New ServerConnection(remoteSvrName)  
      srvConn2.LoginSecure = False  
      srvConn2.Login = sqlServerLogin  
      srvConn2.Password = password  
      Dim srv3 As New Server(srvConn2)  
      Console.WriteLine(srv3.Information.Version)   ' connection is established  
   End Sub  
End Class  
```  
  
## <a name="connecting-to-an-instance-of-sql-server-by-using-sql-server-authentication-in-visual-c"></a>Conectarse a una instancia de SQL Server mediante la autenticación de SQL Server en Visual C#  
 Al conectarse a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], debe especificar el tipo de autenticación. En este ejemplo se muestra un método alternativo para declarar una variable de objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>, que permite reutilizar la información de conexión.  
  
 El ejemplo es el código de Visual C# .NET que se muestra cómo conectarse a la instancia remota y *vPassword* contienen el inicio de sesión y la contraseña.  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll  
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {   
      String sqlServerLogin = "user_id";  
      String password = "pwd";  
      String instanceName = "instance_name";  
      String remoteSvrName = "remote_server_name";  
  
      // Connecting to an instance of SQL Server using SQL Server Authentication  
      Server srv1 = new Server();   // connects to default instance  
      srv1.ConnectionContext.LoginSecure = false;   // set to true for Windows Authentication  
      srv1.ConnectionContext.Login = sqlServerLogin;  
      srv1.ConnectionContext.Password = password;  
      Console.WriteLine(srv1.Information.Version);   // connection is established  
  
      // Connecting to a named instance of SQL Server with SQL Server Authentication using ServerConnection  
      ServerConnection srvConn = new ServerConnection();  
      srvConn.ServerInstance = @".\" + instanceName;   // connects to named instance  
      srvConn.LoginSecure = false;   // set to true for Windows Authentication  
      srvConn.Login = sqlServerLogin;  
      srvConn.Password = password;  
      Server srv2 = new Server(srvConn);  
      Console.WriteLine(srv2.Information.Version);   // connection is established  
  
      // For remote connection, remote server name / ServerInstance needs to be specified  
      ServerConnection srvConn2 = new ServerConnection(remoteSvrName);  
      srvConn2.LoginSecure = false;  
      srvConn2.Login = sqlServerLogin;  
      srvConn2.Password = password;  
      Server srv3 = new Server(srvConn2);  
      Console.WriteLine(srv3.Information.Version);   // connection is established  
   }  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  
