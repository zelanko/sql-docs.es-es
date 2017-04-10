---
title: "Obtener acceso al proveedor WMI de Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "11/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
apiname: 
  - "Reporting Services WMI Provider"
apilocation: 
  - "reportingservices.mof"
helpviewer_keywords: 
  - "proveedor WMI [Reporting Services]"
  - "programación [Reporting Services]"
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
caps.latest.revision: 57
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 57
---
# Obtener acceso al proveedor WMI de Reporting Services
  El proveedor WMI de Reporting Services expone dos clases de WMI para administrar instancias del servidor de informes en modo nativo mediante scripts:  
  
> [!IMPORTANT]  
>  A partir de la versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , el proveedor WMI se admite para los servidores de informes en modo nativo. Los servidores de informes en modo de SharePoint pueden administrarse con las páginas de Administración central de SharePoint y scripts de PowerShell.  
  
|Clase|Espacio de nombres|Description|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName>*\v13|Proporciona la información básica requerida para que un cliente se conecte a un servidor de informes instalado.|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\RS_*\<EncodedInstanceName>*\v13\Admin|Representa la instalación y los parámetros de tiempo de ejecución de una instancia del servidor de informes. Estos parámetros se guardan en el archivo de configuración del servidor de informes.<br /><br /> **\*\* Importante \*\*** Esta clase solo está disponible con privilegios de administrador.|  
  
 Se crea una instancia de cada una de las clases anteriores para cada instancia del servidor de informes. Puede utilizar cualquier herramienta de Microsoft o de terceros para tener acceso a los objetos de WMI expuestos por el servidor de informes, incluidas las interfaces de programación de WMI, expuestas por .NET Framework. En este tema se describe cómo acceder y usar las instancias de clases WMI con el comando de PowerShell [Get-WmiObject](http://technet.microsoft.com/library/dd315295.aspx).  
  
## Determinar el nombre de instancia en la cadena del espacio de nombres  
 El nombre de instancia de la ruta de acceso del espacio de nombres para las clases de WMI de Reporting Services es una codificación de los nombres de instancia especificados al instalar las instancias con nombre de Reporting Services. Concretamente, los caracteres especiales en los nombres de instancia se codifican. Por ejemplo, el carácter de subrayado (_) se codifica como “_5f”, por lo que el nombre de instancia “My_Instance” se codificará como “My_5fInstance” en la ruta de acceso del espacio de nombres de WMI.  
  
 Para enumerar los nombres de instancia codificados de las instancias del servidor de informes en la ruta de acceso del espacio de nombres de WMI, utilice el siguiente comando de PowerShell:  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace root\Microsoft\SqlServer\ReportServer  –class __Namespace –ComputerName hostname | select Name  
```  
  
## Obtener acceso a clases de WMI mediante PowerShell  
 Para obtener acceso a las clases de WMI, ejecute el siguiente comando:  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace <namespacename> –class <classname> –ComputerName <hostname>  
```  
  
 Por ejemplo, para tener acceso a la clase MSReportServer_ConfigurationSetting en la instancia predeterminada del servidor de informes del host myrshost, ejecute el siguiente comando. La instancia predeterminada del servidor de informes se debe instalar en myrshost para que el comando se ejecute correctamente.  
  
```  
PS C:\windows\system32> Get-WmiObject –namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 Esta sintaxis de comando genera todos los nombres de propiedad y valores de la clase. Observe que se devuelven todas las instancias de la clase MSReportServer_ConfigurationSetting, aunque esté obteniendo acceso a la clase en el espacio de nombres de la instancia predeterminada del servidor de informes (RS_MSSQLSERVER). Por ejemplo, si myrshost se instala con la instancia predeterminada del servidor de informes y una instancia con nombre del servidor de informes denominada SHAREPOINT, este comando devolverá dos objetos de WMI y generará los nombres de propiedad y valores para ambas instancias del servidor de informes.  
  
 Para que se devuelva una instancia de clase específica cuando se devuelven varias instancias, utilice el parámetro -–Filter para filtrar los resultados en función de propiedades con valores únicos, como InstanceName. Por ejemplo, para devolver solo el objeto de WMI de la instancia predeterminada del servidor de informes, use el siguiente comando:  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='MSSQLSERVER'"  
```  
  
## Consultar los métodos y propiedades disponibles  
 Para ver qué métodos y propiedades están disponibles en una de las clases de WMI de Reporting Services, canalice los resultados desde Get-WmiObject al comando Get-Member. Por ejemplo:  
  
```  
PS C:\windows\system32> Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
## Utilizar un método o propiedad de WMI  
 Una vez tenga los objetos de WMI en las clases de Reporting Services y conozca los métodos y propiedades disponibles, podrá usar esos métodos y propiedades. Por ejemplo, si tiene una instancia con nombre del servidor de informes en modo integrado de SharePoint denominada SHAREPOINT, use la siguiente secuencia de comandos para recuperar la dirección URL del sitio de Administración central de SharePoint:  
  
```  
PS C:\windows\system32> $rsconfig = Get-WmiObject -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v13\Admin" -class MSReportServer_ConfigurationSetting -ComputerName myrshost -filter "InstanceName='SHAREPOINT'"  
PS C:\windows\system32> $rsconfig.GetAdminSiteUrl()  
  
```  
  
## Vea también  
 [Referencia de la biblioteca de proveedores WMI de Reporting Services &#40;SSRS&#41;](../../reporting-services/wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  