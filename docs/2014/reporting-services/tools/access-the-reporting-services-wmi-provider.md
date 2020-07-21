---
title: Acceso al proveedor WMI de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efbe03a4aab65f792b352eeb5b6c5130c4c32335
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783205"
---
# <a name="access-the-reporting-services-wmi-provider"></a>Obtener acceso al proveedor WMI de Reporting Services
  El proveedor WMI de Reporting Services expone dos clases de WMI para administrar instancias del servidor de informes en modo nativo mediante scripts:  
  
> [!IMPORTANT]  
>  A partir de la versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , el proveedor WMI se admite para los servidores de informes en modo nativo. Los servidores de informes en modo de SharePoint pueden administrarse con las páginas de Administración central de SharePoint y scripts de PowerShell.  
  
|Clase|Espacio de nombres|Descripción|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\microsoft\sqlserver\reportserver\ RS_*\<nombredeinstanciacodificada>* \v11|Proporciona la información básica requerida para que un cliente se conecte a un servidor de informes instalado.|  
|MSReportServer_ConfigurationSetting|root\microsoft\sqlserver\reportserver\ RS_*\<nombredeinstanciacodificada>* \v11\Admin|Representa la instalación y los parámetros de tiempo de ejecución de una instancia del servidor de informes. Estos parámetros se guardan en el archivo de configuración del servidor de informes.<br /><br /> **\*\* Importante \*\*** Esta clase solo está disponible con privilegios de administrador.|  
  
 Se crea una instancia de cada una de las clases anteriores para cada instancia del servidor de informes. Puede utilizar cualquier herramienta de Microsoft o de terceros para tener acceso a los objetos de WMI expuestos por el servidor de informes, incluidas las interfaces de programación de WMI, expuestas por .NET Framework. En este tema se describe cómo acceder y usar las instancias de clases WMI con el comando de PowerShell [Get-WmiObject](https://technet.microsoft.com/library/dd315295.aspx).  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>Determinar el nombre de instancia en la cadena del espacio de nombres  
 El nombre de instancia de la ruta de acceso del espacio de nombres para las clases de WMI de Reporting Services es una codificación de los nombres de instancia especificados al instalar las instancias con nombre de Reporting Services. Concretamente, los caracteres especiales en los nombres de instancia se codifican. Por ejemplo, el carácter de subrayado (_) se codifica como "_5f", por lo que el nombre de instancia "My_Instance" se codificará como "My_5fInstance" en la ruta de acceso del espacio de nombres de WMI.  
  
 Para enumerar los nombres de instancia codificados de las instancias del servidor de informes en la ruta de acceso del espacio de nombres de WMI, utilice el siguiente comando de PowerShell:  
  
```powershell
Get-WmiObject -Namespace root\Microsoft\SqlServer\ReportServer -Class __Namespace -ComputerName hostname | Select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>Obtener acceso a clases de WMI mediante PowerShell  
 Para obtener acceso a las clases de WMI, ejecute el siguiente comando:  
  
```powershell
Get-WmiObject -Namespace <namespacename> -Class <classname> -ComputerName <hostname>  
```  
  
 Por ejemplo, para tener acceso a la clase MSReportServer_ConfigurationSetting en la instancia predeterminada del servidor de informes del host myrshost, ejecute el siguiente comando. La instancia predeterminada del servidor de informes se debe instalar en myrshost para que el comando se ejecute correctamente.  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 Esta sintaxis de comando genera todos los nombres de propiedad y valores de la clase. Observe que se devuelven todas las instancias de la clase MSReportServer_ConfigurationSetting, aunque esté obteniendo acceso a la clase en el espacio de nombres de la instancia predeterminada del servidor de informes (RS_MSSQLSERVER). Por ejemplo, si myrshost se instala con la instancia predeterminada del servidor de informes y una instancia con nombre del servidor de informes denominada SHAREPOINT, este comando devolverá dos objetos de WMI y generará los nombres de propiedad y valores para ambas instancias del servidor de informes.  
  
 Para que se devuelva una instancia de clase específica cuando se devuelven varias instancias, use el parámetro -Filter para filtrar los resultados en función de propiedades con valores únicos, como InstanceName. Por ejemplo, para devolver solo el objeto de WMI de la instancia predeterminada del servidor de informes, use el siguiente comando:  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost -Filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>Consultar los métodos y propiedades disponibles  
 Para ver qué métodos y propiedades están disponibles en una de las clases de WMI de Reporting Services, canalice los resultados desde Get-WmiObject al comando Get-Member. Por ejemplo:  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
 Para obtener documentación sobre las propiedades y los métodos de las clases de Reporting Services WMI, vea....  
  
## <a name="use-a-wmi-method-or-property"></a>Utilizar un método o propiedad de WMI  
 Una vez tenga los objetos de WMI en las clases de Reporting Services y conozca los métodos y propiedades disponibles, podrá usar esos métodos y propiedades. Por ejemplo, si tiene una instancia con nombre del servidor de informes en modo integrado de SharePoint denominada SHAREPOINT, use la siguiente secuencia de comandos para recuperar la dirección URL del sitio de Administración central de SharePoint:  
  
```powershell
$rsconfig = Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost -Filter "InstanceName='SHAREPOINT'"  
$rsconfig.GetAdminSiteUrl()  
```  
  
## <a name="see-also"></a>Consulte también
 [Reporting Services referencia de la biblioteca del proveedor WMI &#40;SSRS&#41;](../wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
