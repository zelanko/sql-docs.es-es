---
title: Codificar una tarea personalizada | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Validate method
- custom tasks [Integration Services], validating
- validation [Integration Services], design-time tasks
- SSIS custom tasks, validating
ms.assetid: dc224f4f-b339-4eb6-a008-1b4fe0ea4fd2
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c4fd06d10d2ecd2796d0b12707c5e34168941c7c
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="coding-a-custom-task"></a>Codificar una tarea personalizada
  Una vez que haya creado una clase que herede de la clase base <xref:Microsoft.SqlServer.Dts.Runtime.Task> y haya aplicado el atributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> a la clase, debe invalidar la implementación de las propiedades y los métodos de la clase base para proporcionar su funcionalidad personalizada.  
  
## <a name="configuring-the-task"></a>Configurar la tarea  
  
### <a name="validating-the-task"></a>Validar la tarea  
 Al diseñar un paquete de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], puede usar la validación para comprobar la configuración en cada tarea, de manera que pueda detectar los valores incorrectos o inadecuados en cuanto se establezcan, en lugar de buscar todos los errores solo en tiempo de ejecución. El propósito de la validación es determinar si la tarea contiene conexiones o valores no válidos que impedirán que se ejecute correctamente. De esta manera se garantiza que el paquete contiene tareas con muchas posibilidades de que se ejecuten en su primera ejecución.  
  
 Puede implementar la validación mediante el uso de la **validar** método en el código personalizado. El motor en tiempo de ejecución valida una tarea mediante una llamada a la **validar** método en la tarea. Es responsabilidad del programador de la tarea definir los criterios que dan como correcta o errónea una validación de tarea, así como notificar el motor en tiempo de ejecución del resultado de esta evaluación.  
  
#### <a name="task-abstract-base-class"></a>Clase base abstracta Task  
 El <xref:Microsoft.SqlServer.Dts.Runtime.Task> proporciona la clase base abstracta el **validar** método que invalida cada tarea para definir sus criterios de validación. El [!INCLUDE[ssIS](../../../includes/ssis-md.md)] diseñador llama automáticamente a la **validar** método varias veces durante el diseño del paquete y proporciona indicaciones visuales al usuario cuando se producen advertencias o errores ayudar a identificar problemas con la configuración de la tarea. Las tareas proporcionan los resultados de la validación devolviendo un valor de la enumeración <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> y provocando eventos de errores y advertencias. Estos eventos contienen información que se muestra al usuario en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
 A continuación, se enumeran algunos ejemplos de validación:  
  
-   Un administrador de conexiones valida el nombre de archivo específico.  
  
-   Un administrador de conexiones valida que el tipo de entrada es el tipo esperado, como un archivo XML.  
  
-   Una tarea que espera la base de datos de entrada comprueba que no puede recibir datos de una conexión que no corresponde a una base de datos.  
  
-   Una tarea garantiza que ninguno de sus propiedades contradice otras propiedades establecidas en la misma tarea.  
  
-   Una tarea garantiza que están disponibles todos los recursos necesarios que usa la tarea en tiempo de ejecución.  
  
 El rendimiento es algo que hay que tener en cuenta para determinar lo que se valida y lo que no. Por ejemplo, la entrada para una tarea podría ser una conexión a través de una red que tiene poco ancho banda o mucha intensidad de tráfico. La validación puede tardar varios segundos para procesar si decide validar que el recurso está disponible. Otra validación puede producir un viaje de ida y vuelta (round trip) a un servidor de gran demanda y la rutina de validación podría ser lenta. Aunque hay muchas propiedades y configuraciones que se pueden validar, no se debería validar todo.  
  
-   El código en el **validar** también llama al método el <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> antes de ejecuta la tarea y el <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> cancela la ejecución si se produce un error de validación.  
  
#### <a name="user-interface-considerations-during-validation"></a>Consideraciones de interfaz de usuario durante la validación  
 El <xref:Microsoft.SqlServer.Dts.Runtime.Task> incluye un <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> interfaz como un parámetro a la **validar** método. La interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> contiene los métodos a los que llama la tarea para producir eventos en el motor en tiempo de ejecución. Se llama a los métodos <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> y <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> cuando se produce una advertencia o condición de error durante la validación. Ambos métodos de advertencia requieren los mismos parámetros que incluyen un código de error, componente de origen, descripción, archivo de Ayuda e información de contexto de ayuda. El Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] usa esta información para mostrar indicaciones visuales en la superficie de diseño. Las indicaciones visuales que proporciona el diseñador incluyen un icono de exclamación que aparece junto a la tarea en la superficie del diseñador. Esta indicación visual muestra al usuario que la tarea requiere configuración adicional antes de que la ejecución pueda continuar.  
  
 El icono de exclamación también muestra una información sobre herramientas que contiene un mensaje de error. La tarea proporciona el mensaje de error en el parámetro de descripción del evento. También se muestran mensajes de error en la **lista de tareas** panel de [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], ofrece al usuario una ubicación central para ver todos los errores de validación.  
  
#### <a name="validation-example"></a>Ejemplo de validación  
 En el ejemplo de código siguiente se muestra una tarea con un **nombre de usuario** propiedad. Esta propiedad se ha especificado como la propiedad necesaria para que la validación sea correcta. Si no se establece la propiedad, la tarea expone un error y devuelve <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Failure> de la enumeración <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>. El **validar** método se ajusta en un bloque try/catch y se produce un error de validación si se produce una excepción.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string userName = "";  
  
  public override DTSExecResult Validate(Connections connections,  
     VariableDispenser variableDispenser, IDTSComponentEvents events,  
     IDTSLogging log)  
  {  
    try  
    {  
      if (this.userName == "")  
      {  
        //   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0);  
        //   Fail validation.  
        return DTSExecResult.Failure;  
      }  
      //   Return success.  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string UserName  
  {  
    get  
    {  
      return this.userName;  
    }  
    set  
    {  
      this.userName = value;  
    }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _userName As String = ""  
  
  Public Overrides Function Validate(ByVal connections As Connections, _  
     ByVal variableDispenser As VariableDispenser, _  
     ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging) As DTSExecResult  
  
    Try  
      If Me._userName = "" Then  
        '   Raise an OnError event.  
        events.FireError(0, "SampleTask", "The UserName property must be configured.", "", 0)  
        '   Fail validation.  
        Return DTSExecResult.Failure  
      End If  
      '   Return success.  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture exceptions, post an error, and fail validation.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property UserName() As String  
    Get  
      Return Me._userName  
    End Get  
    Set(ByVal Value As String)  
      Me._userName = Value  
    End Set  
  End Property  
  
End Class  
```  
  
### <a name="persisting-the-task"></a>Conservar la tarea  
 Normalmente, no tiene que implementar la persistencia personalizada para una tarea. Solo se requiere la persistencia personalizada cuando las propiedades de un objeto usan tipos de datos complejos. Para obtener más información, consulte [desarrollar objetos personalizados para Integration Services](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md).  
  
## <a name="executing-the-task"></a>Ejecutar la tarea  
 Esta sección describe cómo utilizar el **Execute** método que heredan e invalidan las tareas. En esta sección también se explican varias maneras de proporcionar información sobre los resultados de la ejecución de la tarea.  
  
### <a name="execute-method"></a>Método Execute  
 Las tareas que se encuentran en un paquete ejecutan cuando el [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] en tiempo de ejecución llama sus **Execute** método. Tareas implementan su lógica de negocios básica y la funcionalidad de este método y proporcionar los resultados de ejecución mediante la publicación de mensajes, que devuelve un valor de la <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> enumeración e invalidar la propiedad **obtener** de la **ExecutionValue** propiedad.  
  
 La clase base <xref:Microsoft.SqlServer.Dts.Runtime.Task> proporciona una implementación predeterminada del método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>. Las tareas personalizadas invalidan este método para definir su funcionalidad en tiempo de ejecución. El objeto <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> ajusta la tarea, aislándola del motor en tiempo de ejecución y de los demás objetos del paquete. Debido a este aislamiento, la tarea no es consciente de su ubicación en el paquete con respecto a su orden de ejecución, y se ejecuta únicamente cuando se llama por el tiempo de ejecución. Esta arquitectura evita los problemas que se pueden producir cuando las tareas modifican el paquete durante la ejecución. La tarea proporciona acceso a los demás objetos del paquete únicamente a través de los objetos que se le suministran como parámetros en el método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>. Estos parámetros permiten que las tareas produzcan eventos, escriban las entradas en el registro de eventos, tengan acceso a la colección de variables y den de alta las conexiones a los orígenes de datos en transacciones, a la vez que se mantiene todavía el aislamiento necesario para garantizar la estabilidad y confiabilidad del paquete.  
  
 En la tabla siguiente se enumeran los parámetros que se proporcionan a la tarea en el método <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>.  
  
|Parámetro|Description|  
|---------------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.Connections>|Contiene una colección de objetos <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> disponibles para la tarea.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.VariableDispenser>|Contiene las variables disponibles para la tarea. Las tareas usan variables a través de VariableDispenser; las tareas no usan directamente las variables. VariableDispenser bloquea y desbloquea las variables y evita los interbloqueos o sobrescrituras.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents>|Contiene los métodos que la tarea llama para producir eventos en el motor en tiempo de ejecución.|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSLogging>|Contiene los métodos y propiedades que usa la tarea para escribir entradas en el registro de eventos.|  
|Object|Contiene el objeto de transacción del que forma parte el contenedor, si existe. Este valor se pasa como un parámetro al método <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager.AcquireConnection%2A> de un objeto <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.|  
  
### <a name="providing-execution-feedback"></a>Proporcionar comentarios de ejecución  
 Las tareas ajustan su código en **try/catch** bloques para evitar las excepciones que se produzca al motor en tiempo de ejecución. Esto asegura que el paquete termina la ejecución y no se detiene de forma inesperada. Sin embargo, el motor en tiempo de ejecución proporciona otros mecanismos para controlar las condiciones de error que se pueden producir durante la ejecución de una tarea. Estos mecanismos incluyen la exposición de mensajes de error y advertencia, la devolución de un valor de la estructura <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult>, la exposición de mensajes, la devolución del valor <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> y la divulgación de información acerca de los resultados de ejecución de la tarea a través de la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.Task.ExecutionValue%2A>.  
  
 La interfaz <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> contiene los métodos <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> y <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A>, a los que la tarea puede llamar para exponer mensajes de error y advertencia en el motor en tiempo de ejecución. Ambos métodos requieren parámetros como el código de error, componente de origen, descripción, archivo de Ayuda e información de contexto de ayuda. Dependiendo de la configuración de la tarea, el tiempo de ejecución responde a estos mensajes provocando eventos y puntos de interrupción o escribiendo información en el registro de eventos.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> también facilita la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> que se usa para proporcionar la información adicional sobre los resultados de ejecución. Por ejemplo, si una tarea elimina las filas de una tabla como parte de su **Execute** método, puede utilizar para devolver el número de filas eliminadas como el valor de la <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> propiedad. Además, <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> proporciona la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecValueVariable%2A>. Esta propiedad permite al usuario asignar la propiedad <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> que devuelve la tarea a cualquier variable visible en la tarea. En ese momento la variable especificada se puede usar para establecer las restricciones de precedencia entre las tareas.  
  
### <a name="execution-example"></a>Ejemplo de ejecución  
 En el ejemplo de código siguiente se muestra una implementación de la **Execute** método y muestra un invalidado **ExecutionValue** propiedad. La tarea elimina el archivo especificado por el **fileName** propiedad de la tarea. La tarea expone una advertencia si el archivo no existe, o si la **fileName** propiedad es una cadena vacía. La tarea devuelve un **booleano** valor en el <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.ExecutionValue%2A> propiedad para indicar si se eliminó el archivo.  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
public class SampleTask : Task  
{  
  private string fileName = "";  
  private bool fileDeleted = false;  
  
  public override DTSExecResult Execute(Connections cons,  
     VariableDispenser vars, IDTSComponentEvents events,  
     IDTSLogging log, Object txn)  
  {  
    try  
    {  
      if (this.fileName == "")  
      {  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0);  
        this.fileDeleted = false;  
      }  
      else  
      {  
        if (System.IO.File.Exists(this.fileName))  
        {  
          System.IO.File.Delete(this.fileName);  
          this.fileDeleted = true;  
        }  
        else  
          this.fileDeleted = false;  
      }  
      return DTSExecResult.Success;  
    }  
    catch (System.Exception exception)  
    {  
      //   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0);  
      return DTSExecResult.Failure;  
    }  
  }  
  public string FileName  
  {  
    get { return this.fileName; }  
    set { this.fileName = value; }  
  }  
  public override object ExecutionValue  
  {  
    get { return this.fileDeleted; }  
  }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Public Class SampleTask  
  Inherits Task  
  
  Private _fileName As String = ""  
  Private _fileDeleted As Boolean = False  
  
  Public Overrides Function Execute(ByVal cons As Connections, _  
     ByVal vars As VariableDispenser, ByVal events As IDTSComponentEvents, _  
     ByVal log As IDTSLogging, ByVal txn As Object) As DTSExecResult  
  
    Try  
      If Me._fileName = "" Then  
        events.FireWarning(0, "SampleTask", "No file specified.", "", 0)  
        Me._fileDeleted = False  
      Else  
        If System.IO.File.Exists(Me._fileName) Then  
          System.IO.File.Delete(Me._fileName)  
          Me._fileDeleted = True  
        Else  
          Me._fileDeleted = False  
        End If  
      End If  
      Return DTSExecResult.Success  
    Catch exception As System.Exception  
      '   Capture the exception and post an error.  
      events.FireError(0, "Sampletask", exception.Message, "", 0)  
      Return DTSExecResult.Failure  
    End Try  
  
  End Function  
  
  Public Property FileName() As String  
    Get  
      Return Me._fileName  
    End Get  
    Set(ByVal Value As String)  
      Me._fileName = Value  
    End Set  
  End Property  
  
  Public Overrides ReadOnly Property ExecutionValue() As Object  
    Get  
      Return Me._fileDeleted  
    End Get  
  End Property  
  
End Class  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)   
 [Codificar una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)   
 [Desarrollar una interfaz de usuario para una tarea personalizada](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
  
  
