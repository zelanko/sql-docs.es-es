---
title: Instalación de solo archivos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a854de693bce88fcba0de2f1c08e4b0fe296b512
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108842"
---
# <a name="files-only-installation-reporting-services"></a>Instalación de solo archivos (Reporting Services)
  *Instalación de solo archivos* hace referencia a una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la que el programa de instalación crea la estructura de carpetas para los archivos de programa de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , copia los archivos en el disco, registra el servicio Servidor de informes en el equipo local, configura la cuenta de servicio, concede permisos de archivos a la cuenta de servicio y registra el proveedor WMI de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Una instalación de solo archivos incluye las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] siguientes: el servicio Servidor de informes (que hospeda el servicio web del servidor de informes, la aplicación de procesamiento en segundo plano y el Administrador de informes), el Generador de informes, la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y las utilidades de línea de comandos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsconfig.exe, rskeymgmt.exe y rs.exe). No se aplica a las características compartidas como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], que se deben especificar como elementos independientes si desea instalarlos.  
  
 A diferencia de lo que ocurre en otros modos de instalación, un servidor de informes que se instale en modo de solo archivos no es operativo en cuanto el programa de instalación finaliza. Es necesario configurar más valores para poner en línea el servidor de informes por medio del [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="when-to-select-files-only-installation-mode"></a>Cuándo seleccionar el modo de instalación de solo archivos  
 Se debe realizar una instalación de solo archivos cuando:  
  
-   Desee conectar el servidor de informes a una base de datos del servidor de informes remota.  
  
-   Desee instalar el servidor de informes como una instancia con nombre.  
  
-   Tenga requisitos de implementación que incluyan el uso de una configuración o funcionalidad personalizadas, y desee controlar por completo cuándo y cómo se configura el servidor.  
  
-   Instale un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que incluya [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="how-to-perform-a-files-only-installation"></a>Cómo realizar una instalación de solo archivos  
 La instalación de solo archivos es la predeterminada para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Puede especificar una instalación de solo archivos a través de la línea de comandos o en el Asistente para la instalación. En los temas siguientes se ofrecen instrucciones paso a paso:  
  
-   [Instale SQL Server 2014 desde el Asistente para la instalación &#40;&#41;de instalación ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
-   [Instale SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
#### <a name="example-command-line-script"></a>Ejemplo de script de línea de comandos  
 Por claridad, el ejemplo incluye /RSINSTALLMODE = "FilesOnlyMode". Sin embargo, dado que el modo de solo archivos es el predeterminado, puede omitirlo y se seguiría realizando una instalación en modo de solo archivos.  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>Asistente para instalación  
 Al seleccionar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en la página Selección de características, el programa de instalación proporciona una página Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que permite especificar el modo de instalación. Para especificar una instalación de solo archivos, seleccione **Instalar pero no configurar el servidor** en la página Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Comprobar una instalación de Reporting Services](verify-a-reporting-services-installation.md)   
 [Configurar la cuenta de servicio del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una conexión a la base de datos del servidor de informes &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Reporting Services la instalación en modo de SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-reporting-services-sharepoint-mode.md)   
 [Instalar el servidor de informes en modo nativo de Reporting Services](install-reporting-services-native-mode-report-server.md)   
 [Herramientas de Reporting Services](../tools/reporting-services-tools.md)  
  
  
