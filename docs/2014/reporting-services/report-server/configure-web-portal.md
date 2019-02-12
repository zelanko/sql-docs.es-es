---
title: Configurar el Administrador de informes (modo nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 005c9fe0ff5ba3f998e80a93ea19d85c87331403
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56028587"
---
# <a name="configure-report-manager-native-mode"></a>Configurar el Administrador de informes (modo nativo)
  El Administrador de informes es una aplicación front-end web que se usa para ver informes, administrar el contenido del servidor de informes y conceder acceso de usuario a un servidor de informes en modo nativo. El Administrador de informes se instala con el servicio web del servidor de informes en la misma instancia del servidor de informes y, opcionalmente, se configura si se selecciona la opción **Instalar la configuración predeterminada del modo nativo** en el programa de instalación. También puede configurar el Administrador de informes después de haber realizado la instalación. En este tema se proporciona información sobre los siguientes escenarios de configuración del Administrador de informes:  
  
-   [Configurar el Administrador de informes para que use la dirección URL predeterminada](#ConfigureRMURL)  
  
     El Administrador de informes es una aplicación web a la que los usuarios tienen acceso en un explorador web. Como mínimo, debe definir la dirección URL que se usa para abrir la aplicación en una ventana del explorador. La dirección URL está compuesta de un nombre de host, un puerto y un directorio virtual. Los valores predeterminados para esta dirección URL incluyen el nombre de host y los valores de puerto que definió para el servicio web del servidor de informes, más el nombre del directorio virtual **reports** . Si tiene una instancia con nombre, el directorio virtual es **reports_instance**, donde **instance** es el nombre de la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Ejecute el Administrador de informes desde un equipo remoto**. Según la configuración de la red, puede ser necesario habilitar el puerto 80 en los equipos para permitir solicitudes con el Administrador de informes.  
  
    > [!TIP]  
    >  Si intenta tener acceso al Administrador de informes en un equipo remoto y recibe mensajes de error de conexión en el explorador, una causa frecuente es la configuración del firewall. Para obtener más información, vea [Configurar un firewall para el acceso al servidor de informes](configure-a-firewall-for-report-server-access.md).  
  
     Si es necesario, habilite el puerto 80 en ambos equipos para permitir que las solicitudes pasen a través de ese puerto. Para obtener más información, vea [Configurar un firewall para el acceso al servidor de informes](configure-a-firewall-for-report-server-access.md).  
  
-   [Configurar el Administrador de informes para que use una dirección URL específica del servidor de informes](#ConfigureSpecificURL)  
  
     De forma predeterminada, el Administrador de informes se conecta al servicio web del servidor de informes que se ejecuta en el mismo servicio del servidor de informes. El Administrador de informes usa la dirección URL del servicio web del servidor de informes para realizar la conexión. Si define varias direcciones URL para el servicio web del servidor de informes, el Administrador de informes usa la última de ellas. Sin embargo, es posible que en algunas implementaciones le interese que el Administrador de informes se conecte siempre al servicio web a través de una dirección URL estática. Podría interesarle esto si, por ejemplo, hubiese configurado el filtrado de paquetes en un puerto o en una dirección IP específica y deseara que todas las conexiones al servidor de informes pasaran a través de las reglas del filtro que ha definido.  
  
-   [Configurar el Administrador de informes para que use un servidor de informes remoto](#ConfigureRemoteRS)  
  
     De forma predeterminada, el Administrador de informes proporciona acceso front-end al servicio web del servidor de informes que se ejecuta en la misma instancia del servidor, pero puede configurarlo para que se conecte a un servicio web del servidor de informes remoto si desea ejecutar el servicio web y el Administrador de informes en procesos independientes, o si está configurando el acceso a cada servidor de manera diferente (por ejemplo, si está implementando el Administrador de informes para los usuarios de una conexión de extranet o Internet, y desea colocar un firewall entre ambos).  
  
-   [Personalizar los estilos y el título de la aplicación](#ModifyTitle)  
  
     El Administrador de informes, el Visor HTML y la barra de herramientas de informe se pueden personalizar de manera limitada cambiando los estilos y modificando el título de la aplicación que aparece en el Administrador de informes.  
  
-   [Desactivar el Administrador de informes](#DisableRM)  
  
     Al instalar una instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que utiliza el modo nativo, el Administrador de informes se habilita de forma predeterminada. Pero puede desactivarlo si tiene una aplicación front-end personalizada que proporciona una funcionalidad equivalente, si solo quiere usar las interfaces SOAP o Acceso URL para tener acceso al servidor de informes o si usa un Administrador de informes desde una instancia diferente del servidor de informes.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para utilizar el Administrador de informes, debe cumplir los requisitos previos siguientes:  
  
-   Tener un servidor de informes configurado mínimamente. Para obtener más información sobre cómo configurar mínimamente un servidor de informes, vea [Configurar un servidor de informes &#40;modo nativo de Reporting Services&#41;](configure-a-report-server-reporting-services-native-mode.md).  
  
-   El servidor de informes se debe ejecutar en modo nativo. No puede utilizar el Administrador de informes con un servidor de informes configurado para el modo integrado de SharePoint. En SQL Server 2012, no se puede cambiar un servidor de informes de un modo a otro. Si desea cambiar el tipo de servidor de informes que usa su entorno, debe instalar el modo deseado del servidor de informes y, a continuación, copiar o mover los elementos de informe al nuevo servidor de informes. Este proceso se conoce normalmente como "migración". Los pasos necesarios para la migración dependen del modo al que se realice la migración y la versión desde la que se migre. Para obtener más información, vea [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   También debe tener Internet Explorer 7.0 o posterior con scripting habilitado. Para obtener más información, consulte [planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md).  
  
##  <a name="ConfigureRMURL"></a> Configurar el Administrador de informes para que use la dirección URL predeterminada  
 De forma predeterminada, la dirección URL del Administrador de informes consta de un único nombre de directorio virtual, más el puerto y el nombre de host que se han definido para el servicio web del servidor de informes que se ejecuta en la misma instancia. En la mayoría de los casos, el nombre de host es el nombre de red del equipo del servidor de informes, pero también puede ser una dirección IP o un encabezado de host que se resuelva como el equipo. Para configurar el Administrador de informes de modo que use la dirección URL predeterminada, utilice la página **Dirección URL del Administrador de informes** en la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
#### <a name="to-configure-the-default-report-manager-url-and-virtual-directory"></a>Para configurar la dirección URL del Administrador de informes y el directorio virtual predeterminados  
  
1.  Inicie la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes.  
  
2.  En la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , haga clic en **Dirección URL del Administrador de informes** para abrir la página que le permitirá configurar la dirección URL.  
  
3.  Escriba un nombre único de directorio virtual para el Administrador de informes.  
  
4.  Haga clic en **Aplicar**.  
  
5.  Si usa [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] o Windows Server 2008, podrían requerirse pasos adicionales para poder usar el Administrador de informes. Para obtener más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="ConfigureSpecificURL"></a> Configurar el Administrador de informes para que use una dirección URL específica del servidor de informes  
 Cuando se configuran direcciones URL en la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , el Administrador de informes detecta y utiliza automáticamente las direcciones URL nuevas y actualizadas para el servidor de informes que se ejecuta en la misma instancia del servidor. Si su implementación requiere el uso de una única dirección URL estática para todas las solicitudes del servidor de informes, puede especificar dicha dirección en el archivo RSReportServer.config.  
  
#### <a name="to-configure-a-static-report-server-url"></a>Para configurar una dirección URL estática del servidor de informes  
  
1.  Abra el archivo **RsReportServer.config** en un editor de texto. De forma predeterminada, se encuentra en \Archivos de programa\Microsoft SQL Server\MSRS12.\<*nombreDeInstancia*>\Reporting Services\ReportServer.  
  
2.  Busque `ReportServerURL`.  
  
3.  Reemplácelo por la dirección URL de la instancia del servidor de informes.  
  
4.  Guarde los cambios y cierre el archivo.  
  
 Para obtener más información sobre el archivo de configuración, consulte [modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41; ](modify-a-reporting-services-configuration-file-rsreportserver-config.md) y [RSReportServer Configuration File](rsreportserver-config-configuration-file.md).  
  
##  <a name="ConfigureRemoteRS"></a> Configurar el Administrador de informes para que use un servidor de informes remoto  
 En las configuraciones de implementación que sitúan el Administrador de informes y el servidor de informes en equipos diferentes, debe tener dos instalaciones independientes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. El Administrador de informes se incrusta en el servicio del servidor de informes y no se instala solo. Si desea ejecutar el Administrador de informes en otro equipo dentro de su propio proceso, debe instalar un segundo servidor de informes. Ambas instancias del servidor deben ser servidores de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
#### <a name="to-connect-report-manager-to-a-remote-report-server-instance"></a>Para conectar el Administrador de informes a una instancia del servidor de informes remota  
  
1.  Instale dos instancias del servidor de informes.  
  
2.  Configure la primera instalación que hospedará el servidor de informes:  
  
    1.  Inicie la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    2.  Haga clic en **Dirección URL del servicio web** para configurar un nombre de host, un puerto y un directorio virtual para el servidor de informes.  
  
    3.  Haga clic en **Base de datos** para configurar la base de datos del servidor de informes.  
  
3.  Configure la segunda instalación que hospedará el Administrador de informes:  
  
    1.  Inicie la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    2.  Haga clic en **Dirección URL del Administrador de informes** para escribir un nombre de directorio virtual para el Administrador de informes.  
  
     No configure la base de datos. No pruebe las direcciones URL.  
  
4.  En el equipo del Administrador de informes, modifique la configuración en RSReportServer.config para que señale a la instancia del servidor de informes remota. Al iniciarse, el Administrador de informes leerá el archivo de configuración para obtener la dirección URL para el servidor de informes:  
  
    1.  Abra RSReportServer.config en un editor de texto. De forma predeterminada, se encuentra en \Program Files\Microsoft SQL Server\MSRS11. \< *nombreDeInstancia*> \Reporting.  
  
    2.  Busque `ReportServerURL`.  
  
    3.  Reemplácelo por la dirección URL de la instancia del servidor de informes remota.  
  
    4.  Guarde los cambios y cierre el archivo.  
  
5.  > [!TIP]  
    >  Si es necesario, habilite el puerto 80 en ambos equipos para permitir que las solicitudes pasen a través de ese puerto. Para obtener más información, vea [Configurar un firewall para el acceso al servidor de informes](configure-a-firewall-for-report-server-access.md).  
  
6.  Reinicie el servidor de informes.  
  
7.  Abra el Administrador de informes en una ventana del explorador. Si ya estuviera abierto, actualice el explorador para comprobar que el Administrador de informes está conectado al servidor remoto. Debería ver el contenido del servidor de destino.  
  
8.  Desactive las características del servidor que no esté utilizando:  
  
    -   En el equipo del Administrador de informes, desactive `WebServiceAndHTTPAccessEnabled` y `ScheduleEventsAndReportDeliveryEnabled`.  
  
    -   En el equipo del servidor de informes, desactive `ReportManagerEnabled`.  
  
 Para obtener más información sobre cómo desactivar características, vea [Activar o desactivar las características de Reporting Services](turn-reporting-services-features-on-or-off.md).  
  
##  <a name="ModifyTitle"></a> Personalizar estilos o el título de la aplicación  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] no admite la personalización de las hojas de estilos del Administrador de informes. Sin embargo, si tiene conocimientos sobre desarrollo web, puede modificar los estilos bajo su responsabilidad. Para obtener más información sobre qué archivos contienen información de estilo, vea [Personalizar hojas de estilos para el Visor HTML y el Administrador de informes](../customize-style-sheets-for-html-viewer-and-report-manager.md).  
  
 El Administrador de informes tiene un título de aplicación que aparece en la parte superior de la página. De manera predeterminada, el título es **SQL Server Reporting Services**. Este título puede personalizarse. Para cambiar el título, use la página Configuración del sitio del Administrador de informes. Para modificar la configuración de la aplicación en el Administrador de informes, debe estar asignado al rol **Administrador del sistema** , que permite establecer las propiedades en la página Configuración del sitio. Para ver el título de la aplicación, los usuarios deben estar asignados al rol **Usuario del sistema** .  
  
#### <a name="to-modify-application-title"></a>Para modificar el título de la aplicación  
  
1.  Inicie la sesión usando una cuenta que tenga asignados los permisos **Administrador del sistema** en el servidor de informes.  
  
2.  Abra Internet Explorer.  
  
3.  Escriba la dirección URL del Administrador de informes. De forma predeterminada, es http://\<**nombreDeServidor**>/reports, pero si ha instalado Reporting Services como una instancia con nombre, la dirección URL predeterminada será http://\<**nombreDeServidor**>/reports\<**_nombreDeInstancia**>.  
  
4.  Haga clic en **Configuración del sitio**.  
  
5.  En la pestaña **General** , en **Nombre**, reemplace **SQL Server Reporting Services** por otro nombre.  
  
6.  Haga clic en **Aplicar**.  
  
##  <a name="DisableRM"></a> Turn Off Report Manager  
 Puede desactivar el Administrador de informes si tiene una aplicación personalizada que proporciona una funcionalidad equivalente o si está utilizando la aplicación Administrador de informes de otra instancia del servicio. Para desactivar el Administrador de informes, puede modificar el archivo RSReportServer.config.  
  
#### <a name="to-turn-off-report-manager"></a>Para desactivar el Administrador de informes  
  
1.  Abra el archivo RSReportServer.config en un editor de texto. De forma predeterminada, se encuentra en \Program Files\Microsoft SQL Server\MSRS11. \< *nombreDeInstancia*> \Reporting.  
  
2.  Busque **IsReportManagerEnabled**.  
  
3.  Establezca el valor en **False**.  
  
4.  Guarde los cambios y cierre el archivo.  
  
 Para obtener más información sobre cómo modificar el archivo de configuración, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](modify-a-reporting-services-configuration-file-rsreportserver-config.md). Para obtener más información sobre cómo deshabilitar características en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Activar o desactivar las características de Reporting Services](turn-reporting-services-features-on-or-off.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Comprobar una instalación de Reporting Services](../install-windows/verify-a-reporting-services-installation.md)   
 [Personalizar hojas de estilos para el Visor HTML y el Administrador de informes](../customize-style-sheets-for-html-viewer-and-report-manager.md)   
 [Activar o desactivar las características de Reporting Services](turn-reporting-services-features-on-or-off.md)   
 [Administrar un servidor de informes en modo nativo de Reporting Services](manage-a-reporting-services-native-mode-report-server.md)   
 [Archivo de configuración RSReportServer](rsreportserver-config-configuration-file.md)   
 [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
  
  
