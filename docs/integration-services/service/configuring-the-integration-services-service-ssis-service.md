---
title: "Configurar el servicio Integration Services (servicio SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016)"
helpviewer_keywords: 
  - "servicio de Integration Services, configurar"
  - "archivos de configuración [Integration Services]"
  - "servicio [Integration Services], configurar"
  - "archivos de configuración predeterminados"
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
caps.latest.revision: 74
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 70
---
# Configurar el servicio Integration Services (servicio SSIS)
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se basa en un archivo de configuración para sus valores. De manera predeterminada, este archivo de configuración se denomina MsDtsSrvr.ini.xml y se encuentra en la carpeta %Archivos de programa%\Microsoft SQL Server\110\DTS\Binn.  
  
 Normalmente, no tiene que realizar ningún cambio en este archivo de configuración, ni es necesario cambiar su ubicación predeterminada. Sin embargo, tendrá que modificar el archivo de configuración si sus paquetes están almacenados en una instancia con nombre o una instancia remota del [!INCLUDE[ssDE](../../includes/ssde-md.md)], o en varias instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Además, si mueve el archivo de configuración a una ubicación distinta de la predeterminada, tendrá que modificar la clave del Registro que especifica la ubicación del archivo.  
  
## Contenido del archivo de configuración  
 Cuando se instala [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], el proceso de instalación crea e instala el archivo de configuración para el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Este archivo de configuración contiene los siguientes valores:  
  
-   Si se envía a los paquetes un comando de detención cuando se detenga el servicio.  
  
-   Las carpetas raíz que deben mostrarse para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] son MSDB y File System.  
  
-   Los paquetes del sistema de archivos administrados por el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se encuentran en la carpeta %Archivos de programa%\Microsoft SQL Server\110\DTS\Packages.  
  
 Este archivo de configuración también especifica qué base de datos msdb contiene los paquetes que el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] administrará. De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para administrar los paquetes de la base de datos msdb de la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se instala al mismo tiempo que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si no se instala al mismo tiempo una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)], el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para administrar paquetes de la base de datos msdb de la instancia local predeterminada del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
### Ejemplo de archivo de configuración predeterminado  
 En el ejemplo siguiente se muestra un archivo de configuración predeterminado que especifica los valores siguientes:  
  
-   Los paquetes dejan de ejecutarse cuando se detiene el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Las carpetas raíz donde se almacenan los paquetes en [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] son MSDB y Sistema de archivos.  
  
-   El servicio administra paquetes que están almacenados en la base de datos msdb de la instancia local y predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El servicio administra los paquetes que están almacenados en el sistema de archivos en la carpeta Paquetes.  
  
 **Ejemplo de archivo de configuración predeterminado**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## Modificación del archivo de configuración  
 Puede modificar el archivo de configuración para permitir que los paquetes se sigan ejecutando si se detiene el servicio, para mostrar carpetas raíz adicionales en el Explorador de objetos, o para especificar una carpeta distinta o carpetas adicionales del sistema de archivos que deban ser administradas por el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por ejemplo, puede crear carpetas raíz adicionales de tipo, **SqlServerFolder**, para administrar paquetes en las bases de datos msdb de instancias adicionales de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
> [!NOTE]  
>  Algunos caracteres no son válidos en los nombres de carpeta. Los caracteres válidos para los nombres de carpeta se determinan mediante la clase [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] System.IO.Path **de** y el campo **GetInvalidFilenameChars** . El campo **GetInvalidFilenameChars** proporciona una matriz específica de la plataforma de caracteres que no se pueden especificar en los argumentos de la cadena de ruta pasada a los miembros de la clase **Path**. El juego de caracteres no válidos puede variar en función del sistema de archivos. Normalmente, los caracteres no válidos son las comillas ("), el carácter mayor que (<) y la barra vertical (|).  
  
 Sin embargo, tendrá que modificar el archivo de configuración para administrar paquetes que estén almacenados en una instancia con nombre o una instancia remota de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Si no actualiza el archivo de configuración, no puede usar el **Explorador de objetos** de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ver los paquetes que estén almacenados en la base de datos msdb en la instancia con nombre o en la instancia remota. Si intenta utilizar el **Explorador de objetos** para ver estos paquetes, aparece el mensaje de error siguiente:  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 Para modificar el archivo de configuración para el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , se ha de utilizar un editor de texto.  
  
> [!IMPORTANT]  
>  Después de modificar el archivo de configuración del servicio, deberá reiniciar el servicio para usar la configuración del servicio actualizada.  
  
### Ejemplo de archivo de configuración modificado  
 El ejemplo siguiente muestra un archivo de configuración modificado para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Este archivo es para una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominada `InstanceName` en un servidor denominado `ServerName`.  
  
 **Ejemplo de un archivo de configuración modificado para una instancia con nombre de SQL Server**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## Modificación de la ubicación del archivo de configuración  
 La clave del Registro HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\ServiceConfigFile especifica la ubicación y el nombre del archivo de configuración que usa el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. El valor predeterminado de la clave del Registro es C:\Archivos de programa\Microsoft SQL Server\110\DTS\Binn\MsDtsSrvr.ini.xml. Puede actualizar el valor de la clave del Registro para utilizar un nombre y una ubicación diferentes para el archivo de configuración.  
  
> [!CAUTION]  
>  Editar el Registro de forma incorrecta puede originar problemas graves que requieran volver a instalar el sistema operativo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] no puede garantizar la resolución de dichos problemas. Haga una copia de seguridad de los datos importantes antes de modificar el Registro. Para obtener información sobre cómo hacer una copia de seguridad, restaurar y modificar el Registro, vea el artículo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Knowledge Base, [Definición del Registro de Microsoft Windows](http://support.microsoft.com/kb/256986).  
  
 El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] carga el archivo de configuración cuando se inicia el servicio. Si se cambia la entrada del Registro, es preciso reiniciar el servicio.  
  
  