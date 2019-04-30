---
title: Instalación de solo archivos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c76e3e4f1f2e427d8f56c0b832475a22aee6648d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262267"
---
# <a name="files-only-installation-reporting-services"></a>Instalación de solo archivos (Reporting Services)
  *Instalación de solo archivos* hace referencia a una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la que el programa de instalación crea la estructura de carpetas para los archivos de programa de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , copia los archivos en el disco, registra el servicio Servidor de informes en el equipo local, configura la cuenta de servicio, concede permisos de archivos a la cuenta de servicio y registra el proveedor WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Una instalación de solo archivos incluye las siguientes [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] características: Informes de servicio de servidor (que hospeda el servicio Web del servidor de informes, el procesamiento de la aplicación y el Administrador de informes en segundo plano), el generador de informes, el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] herramienta de configuración y el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilidades de línea de comandos (rsconfig.exe, rskeymgmt.exe y RS.exe). No se aplica a las características compartidas como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], que se deben especificar como elementos independientes si desea instalarlos.  
  
 A diferencia de lo que ocurre en otros modos de instalación, un servidor de informes que se instale en modo de solo archivos no es operativo en cuanto el programa de instalación finaliza. Se necesitará más configuración para poner el servidor de informes en línea por medio del [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="when-to-select-files-only-installation-mode"></a>Cuándo seleccionar el modo de instalación de solo archivos  
 Se debe realizar una instalación de solo archivos cuando:  
  
-   Desee conectar el servidor de informes a una base de datos del servidor de informes remota.  
  
-   Desee instalar el servidor de informes como una instancia con nombre.  
  
-   Tenga requisitos de implementación que incluyan el uso de una configuración o funcionalidad personalizadas, y desee controlar por completo cuándo y cómo se configura el servidor.  
  
-   Instale un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que incluya [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="how-to-perform-a-files-only-installation"></a>Cómo realizar una instalación de solo archivos  
 La instalación de solo archivos es la predeterminada para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Puede especificar una instalación de solo archivos a través de la línea de comandos o en el Asistente para la instalación. En los temas siguientes se ofrecen instrucciones paso a paso:  
  
-   [Instalar SQL Server 2014 desde el Asistente para instalación &#40;instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   [Instalar SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
#### <a name="example-command-line-script"></a>Ejemplo de script de línea de comandos  
 Por claridad, el ejemplo incluye /RSINSTALLMODE = "FilesOnlyMode". Sin embargo, dado que el modo de solo archivos es el predeterminado, puede omitirlo y se seguiría realizando una instalación en modo de solo archivos.  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>Asistente para instalación  
 Al seleccionar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la página Selección de características, el programa de instalación proporciona una página Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que permite especificar el modo de instalación. Para especificar una instalación de solo archivos, seleccione **Instalar pero no configurar el servidor** en la página Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Comprobar una instalación de Reporting Services](verify-a-reporting-services-installation.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Instalación en modo de SharePoint de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](install-reporting-services-sharepoint-mode.md)   
 [Instalar el servidor de informes en modo nativo de Reporting Services](install-reporting-services-native-mode-report-server.md)   
 [Herramientas de Reporting Services](../tools/reporting-services-tools.md)  
  
  
