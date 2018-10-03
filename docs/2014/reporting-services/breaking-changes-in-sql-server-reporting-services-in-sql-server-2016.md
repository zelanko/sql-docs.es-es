---
title: Cambios importantes en SQL Server Reporting Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1bc91211f646129ca0686ae5d8bffe2371ba0a57
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076125"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2014"></a>Cambios recientes de SQL Server Reporting Services en SQL Server 2014
  En este tema se describen los principales cambios realizados en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrarlos al actualizar, o en scripts o informes personalizados. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
 **En este tema:**  
  
-   [Cambios importantes de SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
-   [Cambios importantes de SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
-   [Cambios importantes de SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Cambios importantes de Reporting Services  
 Hay ningún [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] cambios importantes en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Cambios importantes de Reporting Services  
  
### <a name="sharepoint-mode-server-references-require-the-sharepoint-site"></a>Las referencias de servidor en modo de SharePoint requiere el sitio de SharePoint  
 No puede buscar o hacer referencia directamente al servidor de informes utilizando el nombre virtual en la ruta de acceso URL. Por ejemplo:  
  
 `http://<Server name>/ReportServer`  
  
 Se requiere que se incluya el sitio de SharePoint en la ruta de acceso URL. Por ejemplo, si el nombre del sitio es “`videos`” y utilizaban el prefijo “`sites`”, la dirección URL parecería similar a la siguiente:  
  
 `http://<Server Name>/sites/videos/_vti_bin/ReportServer`  
  
### <a name="changes-to-sharepoint-mode-command-line-installation"></a>Cambios en la instalación de línea de comandos en modo de SharePoint  
 El valor de entrada **/RSINSTALLMODE** ahora solo funciona con instalaciones en modo nativo y no en instalaciones en modo de SharePoint. Por ejemplo, no se admite lo siguiente en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]: **/RSINSTALLMODE = "DefaultSharePointMode"**. En lugar de ese valor de entrada, use **/RSSHPINSTALLMODE = " DefaultSharePointMode”**.  
  
 La siguiente instrucción es un ejemplo de conjunto completo de parámetros y comandos de instalación: **setup /ACTION=install /FEATURES=SQL,RS /InstanceName=Denali_INST1 …. /RSSHPINSTALLMODE="DefaultSharePointMode"**  
  
 Para obtener más información sobre las instalaciones de línea de comandos, consulte [símbolo instalación de Reporting Services SharePoint Mode y modo nativo](install-windows/install-reporting-services-at-the-command-prompt.md).  
  
### <a name="the-reporting-services-wmi-provider-no-longer-supports-configuration-of-sharepoint-mode"></a>El proveedor WMI de Reporting Services ya no admite la configuración del modo de SharePoint  
 La configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint ahora se completa con los cmdlets de PowerShell y Administración central de SharePoint. La nueva arquitectura del modo de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] usa la arquitectura de servicios de SharePoint. SharePoint no admite interfaces de WMI.  
  
 Estos cambios afectan a la siguiente lista de componentes y flujos de trabajo:  
  
-   Aplicaciones personalizadas que utilizan el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] del proveedor WMI para [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
-   El administrador de configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], rskeymgmt.exe y rsconfig.exe. En lugar de utilizar estas herramientas para la configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] el modo de SharePoint, use Administración Central de SharePoint y PowerShell.  
  
-   SQL Server Management Studio: los clientes no pueden hacer referencia a un servidor con una sintaxis similar a <nombre_de_equipo>/<nombre_de_instancia>. A partir de la versión de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], el método recomendado era utilizar la dirección URL del sitio SharePoint. Por ejemplo, **http://<sharepoint_server>/<sharePoint_site>**. A partir de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], una dirección URL de sitio de SharePoint es la única sintaxis compatible.  
  
### <a name="report-model-designer-is-not-available-in-sql-server-data-tools"></a>El diseñador de modelos de informe no está disponible en las herramientas de datos de SQL Server  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ya no es compatible con proyectos de modelos de informe. El Diseñador de modelos de informe no está disponible en [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. No puede crear nuevos proyectos de modelos de informe o abrir proyectos existentes en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y no se puede crear o actualizar los modelos de informe. Para actualizar los modelos de informe, puede usar [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] o herramientas anteriores. Puede seguir utilizando modelos de informe como orígenes de datos en los informes creados en las herramientas de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] como el Generador de informes y el Diseñador de informes. Sigue estando disponible en el Diseñador de consultas que usa para crear consultas para extraer datos de informe de los modelos de informe [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
##  <a name="bkmk_kj"></a> Cambios importantes de SQL Server 2008 R2 Reporting Services  
 Esta sección describen cambios importantes en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Dado que SQL Server 2008 R2 es una actualización de versión menor de SQL Server 2008, recomendamos también revisar el contenido en la sección de SQL Server 2008.  
  
### <a name="expanded-csv-data-renderer"></a>Representador de datos CSV expandido  
 En [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], el archivo CSV incluye los datos de gráfico y medidor. Es posible que las aplicaciones que dependan de una estructura anterior de los archivos CSV dejen de funcionar debido a las columnas adicionales de gráficos y medidores.  
  
 Para obtener más información, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](report-builder/exporting-to-a-csv-file-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Cambios de comportamiento en SQL Server Reporting Services en SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [¿Qué novedades &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Características desusadas en SQL Server Reporting Services en SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)   
 [Funcionalidad de SQL Server Reporting Services descontinuada en SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
