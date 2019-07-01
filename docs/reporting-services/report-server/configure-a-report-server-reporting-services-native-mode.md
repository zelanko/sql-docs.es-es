---
title: Configurar un servidor de informes (modo nativo de Reporting Services) | Microsoft Docs
ms.date: 06/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5723122c76b02900f6906c03efb807e58ebcc6d9
ms.sourcegitcommit: 3f2936e727cf8e63f38e5f77b33442993ee99890
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2019
ms.locfileid: "67313975"
---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>Configurar un servidor de informes (modo nativo de Reporting Services)
  Según las opciones que seleccione durante la instalación, podría requerirse una configuración adicional para poder utilizar el servidor de informes. Como mínimo, una configuración del servidor de informes consta de lo siguiente:  
  
-   Una cuenta del servicio del servidor de informes (se configura durante la instalación).  
  
-   La dirección URL del servicio web que proporciona acceso al servidor de informes.  
  
-   Una base de datos del servidor de informes que almacena los datos de la aplicación, los informes y otros elementos.  
  
 El programa de instalación configura los valores mínimos si selecciona alguna de las opciones de instalación siguientes: la configuración predeterminada del modo nativo o la configuración predeterminada del modo integrado de SharePoint. Si ha instalado el servidor de informes en modo de solo archivos (esta es la opción **Instalar pero no configurar** del asistente para la instalación), solo se configura la cuenta de servicio. La dirección URL del servicio web y la base de datos del servidor de informes se deben configurar una vez finalizada la instalación.  
  
Se recomienda que configure el portal web para que pueda conceder acceso de usuario al servidor de informes y administrar el contenido del servidor de informes. Si implementa un servidor de informes en modo integrado de SharePoint, utilice el front-end web de un servidor de SharePoint para conceder el acceso.  
  
 Se pueden configurar características adicionales, como el correo electrónico del servidor de informes y la cuenta de ejecución desatendida, según sea necesario. Para más información, vea [Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Para configurar un servidor de informes, utilice la herramienta Configuración de Reporting Services.  
  
## <a name="to-minimally-configure-a-report-server-installation"></a>Para realizar una configuración mínima de una instalación de servidor de informes  
  
1.  Inicie la herramienta de configuración de Reporting Services y conéctese a la instancia del servidor de informes Para obtener instrucciones, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Haga clic en **Dirección URL del servicio web** con el fin de abrir la página para configurar una dirección URL para el servidor de informes. Para obtener instrucciones sobre cómo definir la dirección URL, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3.  Haga clic en **Base de datos** para crear la base de datos del servidor de informes. Para más información, vea [Crear una base de datos del servidor de informes de modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Vuelva a la página **Dirección URL del servicio web** y haga clic en la dirección URL para comprobar que funciona.  
  
5.  Siga las instrucciones de "Pasos siguientes" para completar la implementación.  
  
## <a name="next-steps"></a>Next Steps  
 Para completar la implementación, debería configurar el portal web o la integración de SharePoint. Para obtener más información, consulte [configurar el portal web](../../reporting-services/report-server/configure-web-portal.md).  
  
 Si Firewall de Windows está activado, es probable que el puerto que el servidor de informes está configurado para usar esté cerrado. Una indicación de que un puerto puede estar cerrado es que aparece una página en blanco al intentar abrir el portal web desde un equipo cliente remoto. Para obtener más información acerca de la configuración del firewall, vea [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
 Si usa Windows Vista o Windows Server 2008, se requieren pasos adicionales para poder abrir el portal web de forma local. Para más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 Para comprobar la instalación, cree las carpetas, cargue los elementos y ejecute los informes. Siga las instrucciones de [Comprobar una instalación de Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) para comprobar la instalación.  
  
## <a name="see-also"></a>Vea también  
 [Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [Configurar un servidor de informes para la administración remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)   
 [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
