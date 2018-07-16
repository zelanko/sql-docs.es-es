---
title: Configurar la integración de servicios (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- configuration files [Integration Services]
- service [Integration Services], configuring
- default configuration files
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
caps.latest.revision: 70
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 71a0436edf57e820b7e6b559814f65823d4390eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283681"
---
# <a name="configuring-the-integration-services-service-ssis-service"></a>Configurar el servicio Integration Services (servicio SSIS)
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 El servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se basa en un archivo de configuración para sus valores. De forma predeterminada, el nombre de este archivo de configuración es MsDtsSrvr.ini.xml y el archivo se encuentra en la carpeta %ProgramFiles%\Microsoft SQL Server\120\DTS\Binn.  
  
 Normalmente, no tiene que realizar ningún cambio en este archivo de configuración, ni es necesario cambiar su ubicación predeterminada. Sin embargo, tendrá que modificar el archivo de configuración si sus paquetes están almacenados en una instancia con nombre o una instancia remota del [!INCLUDE[ssDE](../includes/ssde-md.md)], o en varias instancias de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Además, si mueve el archivo de configuración a una ubicación distinta de la predeterminada, tendrá que modificar la clave del Registro que especifica la ubicación del archivo.  
  
## <a name="configuration-file-contents"></a>Contenido del archivo de configuración  
 Cuando se instala [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], el proceso de instalación crea e instala el archivo de configuración para el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Este archivo de configuración contiene los siguientes valores:  
  
-   Si se envía a los paquetes un comando de detención cuando se detenga el servicio.  
  
-   Las carpetas raíz que deben mostrarse para [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] son MSDB y File System.  
  
-   Los paquetes del sistema de archivos que el [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administra el servicio se encuentran disponibles en %ProgramFiles%\Microsoft SQL Server\120\DTS\Packages.  
  
 Este archivo de configuración también especifica qué base de datos msdb contiene los paquetes que el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] administrará. De forma predeterminada, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se configura para administrar los paquetes de la base de datos msdb de la instancia del [!INCLUDE[ssDE](../includes/ssde-md.md)] que se instala al mismo tiempo que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Si no se instala al mismo tiempo una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] , el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] se configura para administrar paquetes de la base de datos msdb de la instancia local predeterminada del [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
### <a name="default-configuration-file-example"></a>Ejemplo de archivo de configuración predeterminado  
 En el ejemplo siguiente se muestra un archivo de configuración predeterminado que especifica los valores siguientes:  
  
-   Los paquetes dejan de ejecutarse cuando se detiene el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Las carpetas raíz donde se almacenan los paquetes en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] son MSDB y Sistema de archivos.  
  
-   El servicio administra paquetes que están almacenados en la base de datos msdb de la instancia local y predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
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
  
## <a name="modification-of-the-configuration-file"></a>Modificación del archivo de configuración  
 Puede modificar el archivo de configuración para permitir que los paquetes se sigan ejecutando si se detiene el servicio, para mostrar carpetas raíz adicionales en el Explorador de objetos, o para especificar una carpeta distinta o carpetas adicionales del sistema de archivos que deban ser administradas por el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Por ejemplo, puede crear carpetas raíz adicionales de tipo, `SqlServerFolder`, para administrar paquetes en las bases de datos msdb de instancias adicionales de [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
> [!NOTE]  
>  Algunos caracteres no son válidos en los nombres de carpeta. Los caracteres válidos para los nombres de carpeta se determinan mediante la clase [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] System.IO.Path **de** y el campo **GetInvalidFilenameChars** . El campo **GetInvalidFilenameChars** proporciona una matriz específica de la plataforma de caracteres que no se pueden especificar en los argumentos de la cadena de ruta pasada a los miembros de la clase **Path** . El juego de caracteres no válidos puede variar en función del sistema de archivos. Normalmente, los caracteres no válidos son las comillas ("), el carácter mayor que (<) y la barra vertical (|).  
  
 Sin embargo, tendrá que modificar el archivo de configuración para administrar paquetes que estén almacenados en una instancia con nombre o una instancia remota de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Si no actualiza el archivo de configuración, no puede usar el **Explorador de objetos** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para ver los paquetes que estén almacenados en la base de datos msdb en la instancia con nombre o en la instancia remota. Si intenta utilizar el **Explorador de objetos** para ver estos paquetes, aparece el mensaje de error siguiente:  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 Para modificar el archivo de configuración para el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , se ha de utilizar un editor de texto.  
  
> [!IMPORTANT]  
>  Después de modificar el archivo de configuración del servicio, deberá reiniciar el servicio para usar la configuración del servicio actualizada.  
  
### <a name="modified-configuration-file-example"></a>Ejemplo de archivo de configuración modificado  
 El ejemplo siguiente muestra un archivo de configuración modificado para [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Este archivo es para una instancia con nombre de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] denominada `InstanceName` en un servidor denominado `ServerName`.  
  
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
  
## <a name="modification-of-the-configuration-file-location"></a>Modificación de la ubicación del archivo de configuración  
La clave del registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\ServiceConfigFile** especifica la ubicación y el nombre de la configuración de archivos que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa el servicio. El valor predeterminado de la clave del registro es **C:\Program Files\Microsoft SQL Server\120\DTS\Binn\MsDtsSrvr.ini.xml**. Puede actualizar el valor de la clave del Registro para utilizar un nombre y una ubicación diferentes para el archivo de configuración. Tenga en cuenta que el número de versión en la ruta de acceso (120 para SQL Server [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]) puede variar en función de la versión de SQL Server. 
  
  
> [!CAUTION]  
>  Editar el Registro de forma incorrecta puede originar problemas graves que requieran volver a instalar el sistema operativo. [!INCLUDE[msCoName](../includes/msconame-md.md)] no puede garantizar que se puedan resolver problemas derivados de la modificación incorrecta del registro. Haga una copia de seguridad de los datos importantes antes de modificar el Registro. Para obtener información sobre cómo hacer una copia de seguridad, restaurar y modificar el Registro, vea el artículo de [!INCLUDE[msCoName](../includes/msconame-md.md)] Knowledge Base, [Definición del Registro de Microsoft Windows](http://support.microsoft.com/kb/256986).  
  
 El servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] carga el archivo de configuración cuando se inicia el servicio. Si se cambia la entrada del Registro, es preciso reiniciar el servicio.  
  
  
