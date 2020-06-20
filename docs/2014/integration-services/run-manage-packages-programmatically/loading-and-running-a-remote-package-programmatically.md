---
title: Cargar y ejecutar mediante programación un paquete remoto | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Integration Services packages, running
- packages [Integration Services], running
- remote packages [Integration Services]
ms.assetid: 9f6ef376-3408-46bf-b5fa-fc7b18c689c9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f0b0340c33f5a53ba75cb42fa16e08b8b45f92da
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964512"
---
# <a name="loading-and-running-a-remote-package-programmatically"></a>Cargar y ejecutar mediante programación un paquete remoto
  Para ejecutar los paquetes remotos desde un equipo local que no tiene instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], inicie los paquetes para que se ejecuten en el equipo remoto en el que está instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para ello, haga que el equipo local use el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un servicio web o un componente remoto para iniciar los paquetes en el equipo remoto. Si intenta iniciar los paquetes remotos directamente desde el equipo local, se cargarán y se intentará ejecutar los paquetes desde el equipo local. Si el equipo local no tiene instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], no se ejecutarán los paquetes.  
  
> [!NOTE]  
>  No puede ejecutar paquetes fuera de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] en un equipo cliente que no tenga instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], y puede que las condiciones de su licencia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no le permitan instalar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en equipos adicionales. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un componente de servidor y no se puede distribuir entre equipos cliente.  
  
 Como alternativa, puede ejecutar un paquete remoto desde un equipo local que tiene instalado [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Para obtener más información, consulte [Loading and Running a Local Package Programmatically](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md) (Cargar y ejecutar un paquete local mediante programación).  
  
##  <a name="running-a-remote-package-on-the-remote-computer"></a><a name="top"></a> Ejecución de un paquete remoto en el equipo remoto  
 Como se ha mencionado anteriormente, hay varias maneras en las que puede ejecutar un paquete remoto en un servidor remoto:  
  
-   [Uso del Agente SQL Server para ejecutar un paquete remoto mediante programación](#agent)  
  
-   [Uso de un servicio web o el componente remoto para ejecutar el paquete remoto mediante programación](#service)  
  
 Casi todos los métodos que se utilizan en este tema para cargar y guardar los paquetes requieren una referencia al ensamblado `Microsoft.SqlServer.ManagedDTS`. La excepción es el enfoque ADO.NET mostrado en este tema para ejecutar el **sp_start_job** procedimiento almacenado, que solo requiere una referencia a `System.Data` . Después de agregar la referencia al ensamblado `Microsoft.SqlServer.ManagedDTS` en un nuevo proyecto, importe el espacio de nombres <xref:Microsoft.SqlServer.Dts.Runtime> con una instrucción `using` o `Imports`.  
  
###  <a name="using-sql-server-agent-to-run-a-remote-package-programmatically-on-the-server"></a><a name="agent"></a> Uso del Agente SQL Server para ejecutar un paquete remoto mediante programación en el servidor  
 En el ejemplo de código siguiente se muestra cómo utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante programación para ejecutar un paquete remoto en el servidor. En el ejemplo de código se llama al procedimiento almacenado del sistema, **sp_start_job**, que inicia un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El trabajo que el procedimiento inicia se denomina `RunSSISPackage` y este trabajo se encuentra en el equipo remoto. El trabajo `RunSSISPackage` ejecuta luego el paquete en el equipo remoto.  
  
> [!NOTE]  
>  El valor devuelto del procedimiento almacenado **sp_start_job** indica si el procedimiento almacenado ha podido iniciar correctamente el trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor devuelto no indica si el paquete se ha iniciado correctamente o no.  
  
 Para obtener información sobre cómo solucionar problemas de los paquetes que se ejecutan desde trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea el artículo de Microsoft [El paquete de SSIS no se ejecuta cuando recibe una llamada de un paso de trabajo del Agente SQL Server](https://support.microsoft.com/kb/918760).  
  
### <a name="sample-code"></a>Código de ejemplo  
  
```vb  
Imports System.Data  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
  
    Dim jobConnection As SqlConnection  
    Dim jobCommand As SqlCommand  
    Dim jobReturnValue As SqlParameter  
    Dim jobParameter As SqlParameter  
    Dim jobResult As Integer  
  
    jobConnection = New SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI")  
    jobCommand = New SqlCommand("sp_start_job", jobConnection)  
    jobCommand.CommandType = CommandType.StoredProcedure  
  
    jobReturnValue = New SqlParameter("@RETURN_VALUE", SqlDbType.Int)  
    jobReturnValue.Direction = ParameterDirection.ReturnValue  
    jobCommand.Parameters.Add(jobReturnValue)  
  
    jobParameter = New SqlParameter("@job_name", SqlDbType.VarChar)  
    jobParameter.Direction = ParameterDirection.Input  
    jobCommand.Parameters.Add(jobParameter)  
    jobParameter.Value = "RunSSISPackage"  
  
    jobConnection.Open()  
    jobCommand.ExecuteNonQuery()  
    jobResult = DirectCast(jobCommand.Parameters("@RETURN_VALUE").Value, Integer)  
    jobConnection.Close()  
  
    Select Case jobResult  
      Case 0  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.")  
      Case Else  
        Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.")  
    End Select  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
namespace LaunchSSISPackageAgent_CS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      SqlConnection jobConnection;  
      SqlCommand jobCommand;  
      SqlParameter jobReturnValue;  
      SqlParameter jobParameter;  
      int jobResult;  
  
      jobConnection = new SqlConnection("Data Source=(local);Initial Catalog=msdb;Integrated Security=SSPI");  
      jobCommand = new SqlCommand("sp_start_job", jobConnection);  
      jobCommand.CommandType = CommandType.StoredProcedure;  
  
      jobReturnValue = new SqlParameter("@RETURN_VALUE", SqlDbType.Int);  
      jobReturnValue.Direction = ParameterDirection.ReturnValue;  
      jobCommand.Parameters.Add(jobReturnValue);  
  
      jobParameter = new SqlParameter("@job_name", SqlDbType.VarChar);  
      jobParameter.Direction = ParameterDirection.Input;  
      jobCommand.Parameters.Add(jobParameter);  
      jobParameter.Value = "RunSSISPackage";  
  
      jobConnection.Open();  
      jobCommand.ExecuteNonQuery();  
      jobResult = (Int32)jobCommand.Parameters["@RETURN_VALUE"].Value;  
      jobConnection.Close();  
  
      switch (jobResult)  
      {  
        case 0:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, started successfully.");  
          break;  
        default:  
          Console.WriteLine("SQL Server Agent job, RunSISSPackage, failed to start.");  
          break;  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
 
  
###  <a name="using-a-web-service-or-remote-component-to-run-a-remote-package-programmatically"></a><a name="service"></a> Uso de un servicio web o el componente remoto para ejecutar el paquete remoto mediante programación  
 La solución anterior para ejecutar los paquetes en ejecución mediante programación en el servidor no requiere ningún código personalizado en el servidor. Sin embargo, quizá prefiera una solución que no confía en el Agente SQL Server para ejecutar los paquetes. En el ejemplo siguiente se muestra un servicio web que se puede crear en el servidor para iniciar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] localmente y una aplicación de prueba que se puede utilizar para llamar al servicio web desde un equipo cliente. Si prefiere crear un componente remoto en lugar de un servicio web, puede utilizar la misma lógica de código con muy pocos cambios en un componente remoto. No obstante, un componente remoto puede requerir una configuración más amplia que un servicio web.  
  
> [!IMPORTANT]  
>  Con la configuración predeterminada para la autenticación y autorización, un servicio web no tiene generalmente los permisos necesarios para obtener acceso a SQL Server o al sistema de archivos para cargar y ejecutar los paquetes. Quizá tenga que asignar los permisos adecuados al servicio web configurando los valores de autenticación y autorización en el archivo **web.config** y asignando los permisos de base de datos y del sistema de archivos según corresponda. Una descripción completa de los permisos de la Web, base de datos y sistema de archivos está más allá del ámbito de este tema.  
  
> [!IMPORTANT]  
>  Los métodos de la clase <xref:Microsoft.SqlServer.Dts.Runtime.Application> para trabajar con el almacén de paquetes SSIS solamente admiten ".", localhost o el nombre del servidor local. No puede utilizar "(local)".  
  
### <a name="sample-code"></a>Código de ejemplo  
 Los ejemplos de código siguientes muestran cómo crear y probar el servicio web.  
  
#### <a name="creating-the-web-service"></a>Crear el servicio web  
 Un paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se puede cargar directamente desde un archivo, directamente desde SQL Server o desde el Almacén de paquetes SSIS, que administra el almacenamiento del paquete en SQL Server y en carpetas del sistema de archivos especiales. En este ejemplo se admiten todas las opciones disponibles utilizando el constructor `Select Case` o `switch` para seleccionar la sintaxis adecuada para iniciar el paquete y concatenar adecuadamente los argumentos de entrada. El método de servicio web LaunchPackage devuelve el resultado de ejecución del paquete como un entero en lugar de un valor <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> para que los equipos cliente no requieran una referencia a ningún ensamblado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
###### <a name="to-create-a-web-service-to-run-packages-on-the-server-programmatically"></a>Para crear un servicio web para ejecutar mediante programación los paquetes en el servidor  
  
1.  Abra Visual Studio y cree un proyecto de servicio web en el lenguaje de programación preferido. En el código de ejemplo se utiliza el nombre LaunchSSISPackageService para el proyecto.  
  
2.  Agregue una referencia a `Microsoft.SqlServer.ManagedDTS` y agregue una `Imports` `using` instrucción o al archivo de código para el espacio de nombres **Microsoft. SqlServer. DTS. Runtime** .  
  
3.  Pegue el código de ejemplo del método de servicio web de LaunchPackage en la clase. (En el ejemplo se muestra el contenido completo de la ventana de código).  
  
4.  Genere y pruebe el servicio web proporcionando un conjunto de valores válidos para los argumentos de entrada del método LaunchPackage que señalan a un paquete existente. Por ejemplo, si package1.dtsx está almacenado en el servidor en C:\My Packages, pase "file" como el valor de sourceType, "C:\My Packages" como el valor de sourceLocation y "package1" (sin la extensión) como el valor de packageName.  
  
```vb  
Imports System.Web  
Imports System.Web.Services  
Imports System.Web.Services.Protocols  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.IO  
  
<WebService(Namespace:="http://dtsue/")> _  
<WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _  
<Global.Microsoft.VisualBasic.CompilerServices.DesignerGenerated()> _  
Public Class LaunchSSISPackageService  
  Inherits System.Web.Services.WebService  
  
  ' LaunchPackage Method Parameters:  
  ' 1. sourceType: file, sql, dts  
  ' 2. sourceLocation: file system folder, (none), logical folder  
  ' 3. packageName: for file system, ".dtsx" extension is appended  
  
  <WebMethod()> _  
  Public Function LaunchPackage( _  
    ByVal sourceType As String, _  
    ByVal sourceLocation As String, _  
    ByVal packageName As String) As Integer 'DTSExecResult  
  
    Dim packagePath As String  
    Dim myPackage As Package  
    Dim integrationServices As New Application  
  
    ' Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName)  
  
    Select Case sourceType  
      Case "file"  
        ' Package is stored as a file.  
        ' Add extension if not present.  
        If String.IsNullOrEmpty(Path.GetExtension(packagePath)) Then  
          packagePath = String.Concat(packagePath, ".dtsx")  
        End If  
        If File.Exists(packagePath) Then  
          myPackage = integrationServices.LoadPackage(packagePath, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid file location: " & packagePath)  
        End If  
      Case "sql"  
        ' Package is stored in MSDB.  
        ' Combine logical path and package name.  
        If integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty) Then  
          myPackage = integrationServices.LoadFromSqlServer( _  
            packageName, "(local)", String.Empty, String.Empty, Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case "dts"  
        ' Package is managed by SSIS Package Store.  
        ' Default logical paths are File System and MSDB.  
        If integrationServices.ExistsOnDtsServer(packagePath, ".") Then  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", Nothing)  
        Else  
          Throw New ApplicationException( _  
            "Invalid package name or location: " & packagePath)  
        End If  
      Case Else  
        Throw New ApplicationException( _  
          "Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.")  
    End Select  
  
    Return myPackage.Execute()  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using System.Web;  
using System.Web.Services;  
using System.Web.Services.Protocols;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.IO;  
  
[WebService(Namespace = "http://dtsue/")]  
[WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]  
public class LaunchSSISPackageServiceCS : System.Web.Services.WebService  
{  
  public LaunchSSISPackageServiceCS()  
  {  
    }  
  
  // LaunchPackage Method Parameters:  
  // 1. sourceType: file, sql, dts  
  // 2. sourceLocation: file system folder, (none), logical folder  
  // 3. packageName: for file system, ".dtsx" extension is appended  
  
  [WebMethod]  
  public int LaunchPackage(string sourceType, string sourceLocation, string packageName)  
  {   
  
    string packagePath;  
    Package myPackage;  
    Application integrationServices = new Application();  
  
    // Combine path and file name.  
    packagePath = Path.Combine(sourceLocation, packageName);  
  
    switch(sourceType)  
    {  
      case "file":  
        // Package is stored as a file.  
        // Add extension if not present.  
        if (String.IsNullOrEmpty(Path.GetExtension(packagePath)))  
        {  
          packagePath = String.Concat(packagePath, ".dtsx");  
        }  
        if (File.Exists(packagePath))  
        {  
          myPackage = integrationServices.LoadPackage(packagePath, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid file location: "+packagePath);  
        }  
        break;  
      case "sql":  
        // Package is stored in MSDB.  
        // Combine logical path and package name.  
        if (integrationServices.ExistsOnSqlServer(packagePath, ".", String.Empty, String.Empty))  
        {  
          myPackage = integrationServices.LoadFromSqlServer(packageName, "(local)", String.Empty, String.Empty, null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      case "dts":  
        // Package is managed by SSIS Package Store.  
        // Default logical paths are File System and MSDB.  
        if (integrationServices.ExistsOnDtsServer(packagePath, "."))  
        {  
          myPackage = integrationServices.LoadFromDtsServer(packagePath, "localhost", null);  
        }  
        else  
        {  
          throw new ApplicationException("Invalid package name or location: "+packagePath);  
        }  
        break;  
      default:  
        throw new ApplicationException("Invalid sourceType argument: valid values are 'file', 'sql', and 'dts'.");  
    }  
  
    return (Int32)myPackage.Execute();  
  
  }  
  
}  
```  
  
#### <a name="testing-the-web-service"></a>Probar el servicio web  
 La aplicación de consola del ejemplo siguiente utiliza el servicio web para ejecutar un paquete. El método LaunchPackage del servicio web devuelve el resultado de ejecución del paquete como un entero en lugar de un valor <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> para que los equipos cliente no requieran una referencia a ningún ensamblado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. En el ejemplo se crea una enumeración privada cuyos valores reflejan los valores <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> para notificar los resultados de ejecución.  
  
###### <a name="to-create-a-console-application-to-test-the-web-service"></a>Para crear una aplicación de consola para probar el servicio web  
  
1.  En Visual Studio, agregue una nueva aplicación de consola, que use el lenguaje de programación preferido, a la misma solución que contiene el proyecto de servicio web. En el código de ejemplo se utiliza el nombre LaunchSSISPackageTest para el proyecto.  
  
2.  Establezca la nueva aplicación de consola como proyecto de inicio de la solución.  
  
3.  Agregue una referencia web del proyecto de servicio web. Si es necesario, ajuste la declaración de variable en el código de ejemplo para el nombre que asigna al objeto proxy del servicio web.  
  
4.  Pegue el código de ejemplo de la rutina Main y la enumeración privada en el código. (En el ejemplo se muestra el contenido completo de la ventana de código).  
  
5.  Modifique la línea de código que llama al método LaunchPackage para proporcionar un conjunto de valores válidos para los argumentos de entrada que señalan a un paquete existente. Por ejemplo, si package1.dtsx está almacenado en el servidor en C:\My Packages, pase "file" como el valor de `sourceType`, "C:\My Packages" como el valor de `sourceLocation` y "package1" (sin la extensión) como el valor de `packageName`.  
  
```vb  
Module LaunchSSISPackageTest  
  
  Sub Main()  
  
    Dim launchPackageService As New LaunchSSISPackageService.LaunchSSISPackageService  
    Dim packageResult As Integer  
  
    Try  
      packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage")  
    Catch ex As Exception  
      ' The type of exception returned by a Web service is:  
      '  System.Web.Services.Protocols.SoapException  
      Console.WriteLine("The following exception occurred: " & ex.Message)  
    End Try  
  
    Console.WriteLine(CType(packageResult, PackageExecutionResult).ToString)  
    Console.ReadKey()  
  
  End Sub  
  
  Private Enum PackageExecutionResult  
    PackageSucceeded  
    PackageFailed  
    PackageCompleted  
    PackageWasCancelled  
  End Enum  
  
End Module  
```  
  
```csharp  
using System;  
  
namespace LaunchSSISPackageSvcTestCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS launchPackageService = new LaunchSSISPackageServiceCS.LaunchSSISPackageServiceCS();  
      int packageResult = 0;  
  
      try  
      {  
        packageResult = launchPackageService.LaunchPackage("sql", String.Empty, "SimpleTestPackage");  
      }  
      catch (Exception ex)  
      {  
        // The type of exception returned by a Web service is:  
        //  System.Web.Services.Protocols.SoapException  
        Console.WriteLine("The following exception occurred: " + ex.Message);  
      }  
  
      Console.WriteLine(((PackageExecutionResult)packageResult).ToString());  
      Console.ReadKey();  
  
    }  
  
    private enum PackageExecutionResult  
    {  
      PackageSucceeded,  
      PackageFailed,  
      PackageCompleted,  
      PackageWasCancelled  
    };  
  
  }  
}  
```  
  

  
## <a name="external-resources"></a>Recursos externos  
  
-   Vídeo: [Cómo automatizar la ejecución de paquetes SSIS usando el Agente SQL Server (vídeo de SQL Server)](https://technet.microsoft.com/sqlserver/ff686764.aspx), en technet.microsoft.com  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de las diferencias entre la ejecución local y remota](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Cargar y ejecutar un paquete local mediante programación](../run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Cargar la salida de un paquete local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
