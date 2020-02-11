---
title: Configurar SQL Server en SMO
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f973b47d4b55624e0f78658f7dfa13ec1aebd80c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74095952"
---
# <a name="configuring-sql-server-in-smo"></a>Configurar SQL Server en SMO
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  En SMO, el <xref:Microsoft.SqlServer.Management.Smo.Information> objeto, el <xref:Microsoft.SqlServer.Management.Smo.Settings> objeto, el <xref:Microsoft.SqlServer.Management.Smo.UserOptions> objeto y el <xref:Microsoft.SqlServer.Management.Smo.Configuration> objeto contienen valores de configuración e información para la instancia [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]de.  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene numerosas propiedades que describen el comportamiento de la instancia instalada. Las propiedades describen las opciones de inicio, los valores predeterminados, archivos y directorios del servidor, la información del procesador y del sistema, el producto y las versiones, la información de conexión, las opciones de memoria, la selección del idioma y de intercalación y el modo de autenticación.  
  
## <a name="sql-server-configuration"></a>Configurar SQL Server  
 Las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Information> contienen información sobre la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], como el procesador y plataforma.  
  
 Las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Settings> contienen información sobre la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se pueden modificar el archivo y directorio predeterminados de la base de datos además del perfil de correo y la cuenta del servidor. Estas propiedades permanecen para la duración de la conexión.  
  
 Las propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> contienen información sobre el comportamiento de las conexiones actuales relacionado con la aritmética, los estándares ANSI y las transacciones.  
  
 Hay también un conjunto de opciones de configuración que está representado por el objeto <xref:Microsoft.SqlServer.Management.Smo.Configuration>. Contiene un conjunto de propiedades que representan las opciones que pueden ser modificadas por el procedimiento almacenado **sp_configure** . Opciones como **aumento de prioridad**, **intervalo de recuperación** y tamaño de paquete de **red**controlan el rendimiento [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]de la instancia de. Se pueden cambiar muchas de estas opciones dinámicamente, pero en algunos casos el valor se configura primero y a continuación se cambia cuando se reinicia la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Hay una propiedad del objeto <xref:Microsoft.SqlServer.Management.Smo.Configuration> para cada opción de configuración. Con el objeto <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> puede modificar la configuración global. Muchas propiedades tienen valores máximos y mínimos que también se almacenan como propiedades de <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>. Estas propiedades requieren que <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> el método confirme el cambio en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El administrador del sistema debe cambiar todas las opciones de configuración en el objeto <xref:Microsoft.SqlServer.Management.Smo.Configuration>.  
  
## <a name="examples"></a>Ejemplos  
 Para los siguientes ejemplos de código, deberá seleccionar el entorno de programación, la plantilla de programación y el lenguaje de programación en los que crear su aplicación. Para obtener más información, vea [crear un proyecto de Visual C&#35; SMO en Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>Modificar las opciones de configuración de SQL Server en Visual Basic  
 En el ejemplo de código se muestra cómo actualizar una opción de configuración en Visual Basic .NET. También recupera y muestra información sobre los valores máximos y mínimos para la opción de configuración especificada. Finalmente, el programa notifica al usuario si la modificación se ha realizado dinámicamente o si se almacena hasta que se reinicie la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display all the configuration options.
Dim p As ConfigProperty
For Each p In srv.Configuration.Properties
    Console.WriteLine(p.DisplayName)
Next
Console.WriteLine("There are " & srv.Configuration.Properties.Count.ToString & " configuration options.")
'Display the maximum and minimum values for ShowAdvancedOptions.
Dim min As Integer
Dim max As Integer
min = srv.Configuration.ShowAdvancedOptions.Minimum
max = srv.Configuration.ShowAdvancedOptions.Maximum
Console.WriteLine("Minimum and Maximum values are " & min & " and " & max & ".")
'Modify the value of ShowAdvancedOptions and run the Alter method.
srv.Configuration.ShowAdvancedOptions.ConfigValue = 0
srv.Configuration.Alter()
'Display when the change takes place according to the IsDynamic property.
If srv.Configuration.ShowAdvancedOptions.IsDynamic = True Then
    Console.WriteLine("Configuration option has been updated.")
Else
    Console.WriteLine("Configuration option will be updated when SQL Server is restarted.")
End If
``` 
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>Modificar la configuración de SQL Server en Visual Basic  
 En el ejemplo de código se muestra información sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la <xref:Microsoft.SqlServer.Management.Smo.Information> instancia <xref:Microsoft.SqlServer.Management.Smo.Settings>de en y, y se <xref:Microsoft.SqlServer.Management.Smo.Settings> modifica <xref:Microsoft.SqlServer.Management.Smo.UserOptions>la configuración de las propiedades del objeto y.  
  
 En el ejemplo el objeto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> y el objeto <xref:Microsoft.SqlServer.Management.Smo.Settings> tienen un método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Puede ejecutar los métodos <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> individualmente para éstos.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display information about the instance of SQL Server in Information and Settings.
Console.WriteLine("OS Version = " & srv.Information.OSVersion)
Console.WriteLine("State = " & srv.Settings.State.ToString)
'Display information specific to the current user in UserOptions.
Console.WriteLine("Quoted Identifier support = " & srv.UserOptions.QuotedIdentifier)
'Modify server settings in Settings.

srv.Settings.LoginMode = ServerLoginMode.Integrated
'Modify settings specific to the current connection in UserOptions.
srv.UserOptions.AbortOnArithmeticErrors = True
'Run the Alter method to make the changes on the instance of SQL Server.
srv.Alter()
```
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>Modificar la configuración de SQL Server en Visual C#  
 En el ejemplo de código se muestra información sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la <xref:Microsoft.SqlServer.Management.Smo.Information> instancia <xref:Microsoft.SqlServer.Management.Smo.Settings>de en y, y se <xref:Microsoft.SqlServer.Management.Smo.Settings> modifica <xref:Microsoft.SqlServer.Management.Smo.UserOptions>la configuración de las propiedades del objeto y.  
  
 En el ejemplo el objeto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> y el objeto <xref:Microsoft.SqlServer.Management.Smo.Settings> tienen un método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Puede ejecutar los métodos <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> individualmente para éstos.  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```csharp  
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>Modificar la configuración de SQL Server en PowerShell  
 En el ejemplo de código se muestra información sobre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la <xref:Microsoft.SqlServer.Management.Smo.Information> instancia <xref:Microsoft.SqlServer.Management.Smo.Settings>de en y, y se <xref:Microsoft.SqlServer.Management.Smo.Settings> modifica <xref:Microsoft.SqlServer.Management.Smo.UserOptions>la configuración de las propiedades del objeto y.  
  
 En el ejemplo el objeto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> y el objeto <xref:Microsoft.SqlServer.Management.Smo.Settings> tienen un método <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. Puede ejecutar los métodos <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> individualmente para éstos.  
  
```powershell 
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>Modificar las opciones de configuración de SQL Server en PowerShell  
 En el ejemplo de código se muestra cómo actualizar una opción de configuración en Visual Basic .NET. También recupera y muestra información sobre los valores máximos y mínimos para la opción de configuración especificada. Finalmente, el programa notifica al usuario si la modificación se ha realizado dinámicamente o si se almacena hasta que se reinicie la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
```powershell 
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = get-item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {    
   "Configuration option has been updated."  
 }  
Else  
{  
    "Configuration option will be updated when SQL Server is restarted."  
}  
```  
  
  
