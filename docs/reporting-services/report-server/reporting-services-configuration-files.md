---
title: Archivos de configuración de Reporting Services | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], configuration files
- configuration options [Reporting Services]
- modifying configuration files
- configuration files [Reporting Services]
ms.assetid: 21e5c32f-ad67-4917-b55a-8e21bd64f5a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 25b695456bbac34e2c6ce8bf8c312c4108dd852e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66506654"
---
# <a name="reporting-services-configuration-files"></a>Archivos de configuración de Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena información de componentes en el Registro y en los archivos de configuración que se copian en el sistema de archivos durante la instalación. Los archivos de configuración contienen una combinación de valores solo para uso interno y valores definidos por el usuario. Estos últimos se especifican durante la instalación, mediante herramientas de configuración, con las utilidades de la línea de comandos y mediante la edición manual de los archivos de configuración.  
  
 Solo es necesario modificar los archivos de configuración cuando se agrega o configura la configuración avanzada. Los parámetros de configuración se especifican como atributos o elementos XML. Si comprende XML y los archivos de configuración, puede utilizar un editor de texto o de código para modificar las opciones de configuración definibles por el usuario. Para más información sobre cómo modificar un archivo de configuración o sobre cómo lee el servidor de informes los valores de configuración nuevos y actualizados, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
> [!NOTE]  
> En versiones anteriores, el Administrador de informes tenía su propio archivo de configuración denominado RSWebApplication.config. Ahora ese archivo está obsoleto. Si actualizó desde una instalación anterior, no se eliminará el archivo pero el servidor de informes no leerá ningún valor del mismo. Si el archivo está en su equipo, debe eliminarlo. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, todas las opciones de configuración del Administrador de informes y del portal web se almacenan y se leen del archivo RSReportServer.config. Para examinar una lista de las configuraciones eliminadas o movidas, vea [Cambios substanciales de SQL Server Reporting Services en SQL Server 2016](../../reporting-services/breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
 En este artículo:  
  
-   [Resumen de archivos de configuración (modo nativo)](#bkmk_config_file_Summary_native_mode)  
  
-   [Resumen de archivos de configuración (modo de SharePoint)](#bkmk_config_file_Summary_sharepoint_mode)  
  
##  <a name="bkmk_config_file_Summary_native_mode"></a> Resumen de archivos de configuración (modo nativo)  
 La tabla siguiente proporciona una descripción de donde está almacenada la configuración. La mayoría de los parámetros de configuración están almacenados en archivos de configuración que se incluyen con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. De forma predeterminada, el directorio de instalación es el siguiente:  
  
''' Instalar rutas de acceso  
C:\Program Files\Microsoft SQL Server\MSRSxx.MSSQLSERVER (donde xx es el número de versión de MS SQL) o  
C:\Program Files\Microsoft SQL Server Reporting Services\SSRS  
  Dependiendo de la versión SSRS
```  
  
|Stored in:|Description|Location|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Stores configuration settings for feature areas of the Report Server service: Report Manager or the web portal, the Report Server Web service, and background processing. For more information about each setting, see [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Stores the code access security policies for the server extensions. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportServer|  
|RSMgrPolicy.config|Stores the code access security policies for the web portal. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Installation directory> \Reporting Services \ReportManager|  
|Web.config for the Report Server Web service|Includes only those settings that are required for ASP.NET.|\<Installation directory> \Reporting Services \ReportServer|  
|Web.config for Report Manager|Includes only those settings that are required for ASP.NET if applicable for the SSRS version.|\<Installation directory> \Reporting Services \ReportManager|  
|ReportingServicesService.exe.config|Stores configuration settings that specify the trace levels and logging options for the Report Server service. For more information about the elements in this file, see [ReportingServicesService Configuration File](../../reporting-services/report-server/reportingservicesservice-configuration-file.md).|\<Installation directory> \Reporting Services \ReportServer \Bin|  
|Registry settings|Stores configuration state and other settings used to uninstall Reporting Services. If you are troubleshooting an installation or configuration problem, you can view these settings to get information about how the report server is configured.<br /><br /> Do not modify these settings directly as this can invalidate your installation.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<InstanceID\> \Setup<br /><br /> **- And -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Services\ReportServer|  
|RSReportDesigner.config|Stores configuration settings for Report Designer. For more information, see [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<drive>:\Program Files \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
|RSPreviewPolicy.config|Stores the code access security policies for the server extensions used during report preview. For more information about this file, see [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|C:\Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssembliesr|  
  
##  <a name="bkmk_config_file_Summary_sharepoint_mode"></a> Summary of configuration Files (SharePoint mode)  
 The following table provides a description of configuration files used for a SharePoint mode report server. Most configuration settings are stored in SharePoint service application databases. For more information, see [Reporting Services SharePoint Service and Service Applications](../../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md).  
  
 By default, the installation directory for SharePoint mode is the following:  
  
```Install path
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
  
|Se almacena en:|Descripción|Ubicación|  
|----------------|-----------------|--------------|  
|RSReportServer.config|Almacena las opciones de configuración para las áreas de característica del servicio del servidor de informes: el Administrador de informes o el portal web, el servicio web del servidor de informes y el procesamiento en segundo plano. Para obtener más información sobre cada configuración, vea [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).|\<Directorio de instalación> \Reporting Services \ReportServer|  
|RSSrvPolicy.config|Almacena las directivas de seguridad de acceso del código para las extensiones del servidor. Para obtener más información acerca de este archivo, vea [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).|\<Directorio de instalación> \Reporting Services \ReportServer|  
|Web.config para el servicio web del servidor de informes.|Incluye solo los valores que son necesarios para ASP.NET si es aplicable para la versión SSRS.|\<Directorio de instalación> \Reporting Services \ReportServer|  
|Parámetros del Registro|Almacena el estado de la configuración y otras configuraciones utilizadas para desinstalar Reporting Services. También almacena información sobre cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .<br /><br /> No modifique directamente estos valores, ya que podría invalidar su instalación.|HKEY_LOCAL_MACHINE \SOFTWARE \Microsoft \Microsoft SQL Server \\<idDeInstancia\> \Setup<br /><br /> Identificador de instancia de ejemplo: MSSQL13.MSSQLSERVER<br /><br /> **- Y -**<br /><br /> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\Reporting Services\Service Applications|  
|RSReportDesigner.config|Almacena los parámetros de configuración para el Diseñador de informes. Para obtener más información, consulte [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md).|\<unidad>:\Archivos de programa \Microsoft Visual Studio 10 \Common7 \IDE \PrivateAssemblies.|  
  
## <a name="see-also"></a>Vea también  
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Extensiones de Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)   
 [rsconfig (utilidad) &#40;SSRS&#41;](../../reporting-services/tools/rsconfig-utility-ssrs.md)   
 [Inicio y detención del servicio del servidor de informes](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
