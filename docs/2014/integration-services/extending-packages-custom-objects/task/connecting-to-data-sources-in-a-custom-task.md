---
title: Conectarse a orígenes de datos de una tarea personalizada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ConnectionManager objects
- connection managers [Integration Services], external data sources
- data sources [Integration Services], external
- custom tasks [Integration Services], external data sources
- external data sources [Integration Services]
- connections [Integration Services], external data sources
- SSIS custom tasks, external data sources
ms.assetid: 9f0b3a43-3eaa-4b3c-bb08-29b630c11306
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76625dc956ff36788f52c5da4106b7ac5eb8c2ab
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381623"
---
# <a name="connecting-to-data-sources-in-a-custom-task"></a>Conectarse a orígenes de datos de una tarea personalizada
  Las tareas se conectan a orígenes de datos externos para recuperar o guardar datos mediante un administrador de conexiones. En tiempo de diseño, un administrador de conexiones representa una conexión lógica y describe información clave como el nombre de servidor y las propiedades de autenticación. En tiempo de ejecución, las tareas llaman al método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> del administrador de conexiones para establecer la conexión física al origen de datos.  
  
 Dado que un paquete puede contener muchas tareas, cada una de los cuales puede tener conexiones a orígenes de datos distintos, el paquete realiza el seguimiento de todos los administradores de conexión de una colección, la colección <xref:Microsoft.SqlServer.Dts.Runtime.Connections>. Las tareas utilizan la colección del paquete para buscar el administrador de conexiones que utilizarán durante la validación y ejecución. La colección <xref:Microsoft.SqlServer.Dts.Runtime.Connections> es el primer parámetro de los métodos <xref:Microsoft.SqlServer.Dts.Runtime.Task.Validate%2A> y <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
 Puede impedir que la tarea use el administrador de conexiones incorrecto mostrando los objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> de la colección al usuario, mediante un cuadro de diálogo o una lista desplegable de la interfaz gráfica de usuario. Esto proporciona al usuario una manera de seleccionar entre únicamente los objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> del tipo adecuado contenidos en el paquete.  
  
 Las tareas llaman al método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> para establecer la conexión física al origen de datos. El método devuelve el objeto de conexión subyacente que la tarea puede usar a continuación. Dado que el administrador de conexiones aísla los detalles de la implementación del objeto de conexión subyacente de la tarea, la tarea solo tiene que llamar al método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> para establecer la conexión y no tiene que preocuparse de otros aspectos de la conexión.  
  
## <a name="example"></a>Ejemplo  
 En el código de ejemplo siguiente se muestra la validación del nombre <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> en los métodos Valide y Execute, y se muestra cómo utilizar el método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> para establecer la conexión física en el método Execute.  
  
```csharp  
private string connectionManagerName = "";  
  
public string ConnectionManagerName  
{  
  get { return this.connectionManagerName; }  
  set { this.connectionManagerName = value; }  
}  
  
public override DTSExecResult Validate(  
  Connections connections, VariableDispenser variableDispenser,  
  IDTSComponentEvents componentEvents, IDTSLogging log)  
{  
  // If the connection manager exists, validation is successful;  
  // otherwise, fail validation.  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception e)  
  {  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
  
public override DTSExecResult Execute(Connections connections,   
  VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,   
  IDTSLogging log, object transaction)  
{  
  try  
  {  
    ConnectionManager cm = connections[this.connectionManagerName];  
    object connection = cm.AcquireConnection(transaction);  
    return DTSExecResult.Success;  
  }  
  catch (System.Exception exception)  
  {  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0);  
    return DTSExecResult.Failure;  
  }  
}  
```  
  
```vb  
Private _connectionManagerName As String = ""  
  
Public Property ConnectionManagerName() As String  
  Get  
    Return Me._connectionManagerName  
  End Get  
  Set(ByVal Value As String)  
    Me._connectionManagerName = value  
  End Set  
End Property  
  
Public Overrides Function Validate( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  ' If the connection manager exists, validation is successful;  
  ' otherwise fail validation.  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Return DTSExecResult.Success  
  Catch e As System.Exception  
    componentEvents.FireError(0, "SampleTask", "Invalid connection manager.", "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
  
Public Overrides Function Execute( _  
  ByVal connections As Microsoft.SqlServer.Dts.Runtime.Connections, _  
  ByVal variableDispenser As Microsoft.SqlServer.Dts.Runtime.VariableDispenser, _  
  ByVal componentEvents As Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents, _  
  ByVal log As Microsoft.SqlServer.Dts.Runtime.IDTSLogging, ByVal transaction As Object) _  
  As Microsoft.SqlServer.Dts.Runtime.DTSExecResult  
  
  Try  
    Dim cm As ConnectionManager = connections(Me._connectionManagerName)  
    Dim connection As Object = cm.AcquireConnection(transaction)  
    Return DTSExecResult.Success  
  Catch exception As System.Exception  
    componentEvents.FireError(0, "SampleTask", exception.Message, "", 0)  
    Return DTSExecResult.Failure  
  End Try  
  
End Function  
```  
  
![Icono de Integration Services (pequeño)](../../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Conexiones de Integration Services &#40;SSIS&#41;](../../connection-manager/integration-services-ssis-connections.md)   
 [Crear administradores de conexiones](../../create-connection-managers.md)  
  
  
