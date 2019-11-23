---
title: URL Administrador de informes (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.rsconfigtool.reportmanagervirtualdirectory.f1
ms.assetid: 45768952-23a6-45a5-b541-e7bf192b4a78
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dd4ff661a10eca71781aee9d1886e80936f6246d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952410"
---
# <a name="report-manager-url-ssrs-native-mode"></a>Dirección URL del Administrador de informes (Modo nativo de SSRS)
  Utilice la página Dirección URL del Administrador de informes para configurar o modificar la dirección URL que se usa para el acceso al Administrador de informes. De forma predeterminada, la dirección URL del Administrador de informes hereda el prefijo, la dirección IP y el puerto de la dirección URL de servicio web del servidor de informes. Esto se debe a que el Administrador de informes proporciona acceso front-end a un servicio web que se ejecuta dentro del mismo servicio del servidor de informes. Si está aislando las aplicaciones de servicio y usa el Administrador de informes para tener acceso a un servicio web del servidor de informes en un equipo diferente, debe modificar el archivo RSReportServer.config para que dirija al Administrador de informes a una instancia diferente. Para obtener más información acerca de cómo configurar una conexión de Administrador de informes a un servidor de informes remoto, vea [ &#40;administrador de configuración de Reporting Services modo&#41;nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Si está configurando el servidor de informes para ejecutarlo en el modo integrado de SharePoint, no cree una dirección URL del Administrador de informes. El Administrador de informes no se admite en un servidor de informes que se ejecuta en el modo integrado de SharePoint. Si ya existe una dirección URL para el Administrador de informes, dejará de estar disponible después de configurar el servidor de informes para ejecutarse en el modo integrado de SharePoint.  
  
 Para abrir esta página, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y haga clic en **Dirección URL del Administrador de informes** en el panel de navegación. Para obtener más información sobre cómo iniciar el Configuration Manager, vea [Administrador de configuración de Reporting Services &#40;modo&#41;nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!NOTE]  
>  Si el Administrador de informes no está habilitado, no puede establecer las opciones de esta página. Para obtener más información sobre cómo habilitar Administrador de informes, vea [ &#40;administrador de configuración de Reporting Services&#41;modo nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Directorio virtual**  
 Especifica el nombre del directorio virtual del Administrador de informes. Solo puede tener un nombre de directorio virtual para cada instancia del Administrador de informes del mismo equipo.  
  
 **URL**  
 Muestra la dirección URL definida para la instancia actual del Administrador de informes.  
  
 **Avanzadas**  
 Agregue una dirección URL adicional para la instancia actual del Administrador de informes.  
  
## <a name="see-also"></a>Vea también  
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Direcciones URL en archivos &#40;de configuración&#41; SSRS Configuration Manager](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)   
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
