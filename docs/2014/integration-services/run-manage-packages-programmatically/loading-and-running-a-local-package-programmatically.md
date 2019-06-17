---
title: Cargar y ejecutar un paquete local mediante programación | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Integration Services packages, running
- events [Integration Services], capturing
- packages [Integration Services], running
- loading packages programmatically
- Visual Basic [Integration Services]
- running packages [Integration Services]
- programmatically load and run packages [SSIS]
ms.assetid: 2f9fc1a8-a001-4c54-8c64-63b443725422
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 00d213bf8ca554b60edc8dc3de3f1290cd00f538
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766897"
---
# <a name="loading-and-running-a-local-package-programmatically"></a>Cargar y ejecutar un paquete local mediante programación
  Puede ejecutar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] según sea necesario o en momentos predeterminados mediante los métodos descritos en [Ejecución de paquetes](../packages/run-integration-services-ssis-packages.md). Sin embargo, con solo unas líneas de código, también puede ejecutar un paquete desde una aplicación personalizada como una aplicación Windows Forms, una aplicación de consola, un formulario Web Forms o servicio web ASP.NET o un servicio de Windows.  
  
 En este tema se describe:  
  
-   Cargar un paquete mediante programación  
  
-   Ejecutar un paquete mediante programación  
  
 Todos los métodos utilizados en este tema para cargar y ejecutar paquetes requieren una referencia al ensamblado `Microsoft.SqlServer.ManagedDTS`. Después de agregar la referencia en un proyecto nuevo, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> con una instrucción `using` o `Imports`.  
  
## <a name="loading-a-package-programmatically"></a>Cargar un paquete mediante programación  
 Para cargar un paquete mediante programación en el equipo local, tanto si el paquete está almacenado localmente como si lo está de forma remota, llame a uno de los métodos siguientes:  
  
|Ubicación de almacenamiento|Método que se llama|  
|----------------------|--------------------|  
|Archivo|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>|  
|Almacén de paquetes SSIS|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>|  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solamente admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
## <a name="running-a-package-programmatically"></a>Ejecutar un paquete mediante programación  
 Al desarrollar una aplicación personalizada en código administrado que ejecuta un paquete en el equipo local, se requiere el enfoque siguiente. Los pasos resumidos aquí se muestran en la aplicación de consola de ejemplo que figura a continuación.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically"></a>Para ejecutar un paquete mediante programación en el equipo local  
  
1.  Inicie el entorno de desarrollo de Visual Studio y cree una nueva aplicación en su lenguaje de desarrollo preferido. En este ejemplo se utiliza una aplicación de consola; sin embargo, también puede ejecutar un paquete de una aplicación Windows Forms, un formulario Web Forms o servicio web ASP.NET o un servicio de Windows.  
  
2.  En el menú **Proyecto**, haga clic en **Agregar referencia** y agregue una referencia a **Microsoft.SqlServer.ManagedDTS.dll**. Haga clic en **Aceptar**.  
  
3.  Usar Visual Basic `Imports` instrucción o C# `using` instrucción para importar el **Microsoft.SqlServer.Dts.Runtime** espacio de nombres.  
  
4.  Agregue el código siguiente en la rutina principal. La aplicación de consola completada se debe parecer al ejemplo siguiente.  
  
    > [!NOTE]  
    >  En el código de ejemplo se muestra cómo cargar el paquete desde el sistema de archivos mediante el método <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>. No obstante, también puede cargar el paquete desde la base de datos MSDB mediante una llamada al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A> o bien desde el almacén de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante una llamada al método <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>.  
  
5.  Ejecute el proyecto. En el código de ejemplo se ejecuta el paquete de ejemplo CalculatedColumns que se instala con los ejemplos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El resultado de la ejecución del paquete se muestra en la ventana de la consola.  
  
### <a name="sample-code"></a>Código muestra  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, Nothing)  
    pkgResults = pkg.Execute()  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, null);  
      pkgResults = pkg.Execute();  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="capturing-events-from-a-running-package"></a>Capturar eventos de un paquete en ejecución  
 Al ejecutar un paquete mediante programación tal como se muestra en el ejemplo anterior, también puede capturar los errores y otros eventos que se producen cuando se ejecuta el paquete. Para ello, agregue una clase que herede de la clase <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> y pase una referencia a dicha clase al cargar el paquete. Aunque en el ejemplo siguiente solamente se captura el evento <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents.OnError%2A>, hay muchos otros eventos que la clase <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> permite capturar.  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically-and-capture-package-events"></a>Para ejecutar un paquete mediante programación en el equipo local y capturar los eventos del paquete  
  
1.  Siga los pasos del ejemplo anterior para crear un proyecto para este ejemplo.  
  
2.  Agregue el código siguiente en la rutina principal. La aplicación de consola completada se debe parecer al ejemplo siguiente.  
  
3.  Ejecute el proyecto. En el código de ejemplo se ejecuta el paquete de ejemplo CalculatedColumns que se instala con los ejemplos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El resultado de la ejecución del paquete se muestra en la ventana de la consola, junto con cualquier error que se produzca.  
  
### <a name="sample-code"></a>Código muestra  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    Dim eventListener As New EventListener()  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, eventListener)  
    pkgResults = pkg.Execute(Nothing, Nothing, eventListener, Nothing, Nothing)  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
  
Class EventListener  
  Inherits DefaultEvents  
  
  Public Overrides Function OnError(ByVal source As Microsoft.SqlServer.Dts.Runtime.DtsObject, _  
    ByVal errorCode As Integer, ByVal subComponent As String, ByVal description As String, _  
    ByVal helpFile As String, ByVal helpContext As Integer, _  
    ByVal idofInterfaceWithError As String) As Boolean  
  
    ' Add application-specific diagnostics here.  
    Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description)  
    Return False  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppWithEventsCS  
{  
  class MyEventListener : DefaultEvents  
  {  
    public override bool OnError(DtsObject source, int errorCode, string subComponent,   
      string description, string helpFile, int helpContext, string idofInterfaceWithError)  
    {  
      // Add application-specific diagnostics here.  
      Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description);  
      return false;  
    }  
  }  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      MyEventListener eventListener = new MyEventListener();  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, eventListener);  
      pkgResults = pkg.Execute(null, null, eventListener, null, null);  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de las diferencias entre la ejecución local y remota](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Cargar y ejecutar un paquete remoto mediante programación](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [Cargar la salida de un paquete local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
