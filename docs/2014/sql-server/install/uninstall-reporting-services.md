---
title: Desinstalar Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 5c764a00-d4bc-465d-b32e-e4efce052ce4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 5b6c7ff7a5ac2539bc6732d68522bb361d6b1b0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62670645"
---
# <a name="uninstall-reporting-services"></a>Desinstalar Reporting Services
  Al desinstalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se quita el contenido que ha creado ni la configuración que ha modificado. No obstante, si hay contenido que necesita una vez completada la desinstalación, se recomienda hacer copias del contenido antes de comenzar el proceso de desinstalación.  
  
## <a name="uninstall-sharepoint-mode"></a>Desinstalar el modo de SharePoint.  
 Al desinstalar el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , se quita lo siguiente:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y proxy del servicio.  
  
-   Archivos usados para la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Las aplicaciones del servicio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se quitan. Si ya no desea las aplicaciones de servicio, puede eliminarlas mediante Windows PowerShell o Administración central de SharePoint.  
  
 Los elementos de informe y los metadatos relacionados no se quitan. Esta información se encuentra en las bases de datos de contenido y configuración relacionadas con aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las bases de datos no se quitan y puede migrarlas manualmente a otra instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint. Si ya no desea la información, elimine las bases de datos. Para obtener más información, vea [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Los siguientes son nombres de ejemplo de las tres bases de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que no se quitan.  
  
-   **Base de datos de servidor de informes:** ReportingService_7f616e2d253040e8ab5653b3c09a065e  
  
-   **Base de datos temporal de informes servidor:** ReportingService_7f616e2d253040e8ab5653b3c09a065eTempDB  
  
-   **Alertas base de datos:** ReportingService_7f616e2d253040e8ab5653b3c09a065e_Alerting  
  
### <a name="uninstall-the-add-in-for-sharepoint-products"></a>Desinstalar el complemento para Productos de SharePoint.  
 Al desinstalar el complemento de un equipo, puede decidir solo la desinstalación de los archivos o también quitar la característica [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de la granja. Para obtener información sobre cómo desinstalar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint, vea [instalar o desinstalar el complemento Reporting Services para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md).  
  
## <a name="uninstall-native-mode"></a>Desinstalar el modo nativo  
 Al desinstalar el modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , cualquier elemento **creado** o **modificado** después de la instalación se deja en su lugar. Para obtener archivos de base de datos, archivos de registro, archivos de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y elementos de contenido de ejemplo como archivos de origen de datos e informes.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es una característica de una instancia y, por lo tanto, no se muestra en el Panel de control de Windows, Programas y Características. Para desinstalar el modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
1.  En el Panel de control de Windows, haga clic en **Programas y características**.  
  
2.  En **Programas y características** , seleccione **Microsoft SQL Server 2012**.  
  
3.  En el asistente para desinstalación, seleccione la instancia que incluye la característica de instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **RS**.  
  
     ![rs_nativemode_uninstall_selectinstance](../../../2014/sql-server/install/media/rs-nativemode-uninstall-selectinstance.gif "rs_nativemode_uninstall_selectinstance")  
  
4.  Tras seleccionar la instancia, seleccione la característica [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
     ![rs_nativemode_uninstall_selectfeatures](../../../2014/sql-server/install/media/rs-nativemode-uninstall-selectfeatures.gif "rs_nativemode_uninstall_selectfeatures")  
  
5.  Finalice el asistente.  
  
## <a name="see-also"></a>Vea también  
 [Desinstalar una instancia existente de SQL Server &#40;programa de instalación&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [Instalar o desinstalar PowerPivot para SharePoint complemento &#40;SharePoint 2013&#41;](../../analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013.md)   
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
