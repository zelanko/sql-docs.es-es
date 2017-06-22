---
title: Configurar el portal web | Documentos de Microsoft
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- the web portal [Reporting Services], configuring
ms.assetid: e918986c-af15-48f6-8178-256aed829c6a
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c0c6cc27711140e96bbf4420e8de596af53ddfcd
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="configure-the-web-portal"></a>Configurar el portal web

el portal web es una aplicación de front-end Web utilizada para ver informes, administrar el contenido del servidor de informes y conceder acceso de usuario a un servidor de informes de modo nativo. el portal web se instala con el servicio Web del servidor de informes en la misma instancia de servidor de informes y, opcionalmente, configura si se selecciona el **instalar en la configuración predeterminada del modo nativo** opción en el programa de instalación. También puede configurar el portal web como una tarea posterior a la instalación. Este tema proporciona información sobre los siguientes los escenarios de configuración del portal web:

## <a name="prerequisites"></a>Requisitos previos

Para utilizar el portal web, debe cumplir los siguientes requisitos previos:

- Tener un servidor de informes configurado mínimamente. Para obtener más información sobre cómo configurar mínimamente un servidor de informes, consulte [configurar un servidor de informes](../../reporting-services/report-server/configure-a-report-server-reporting-services-native-mode.md).

- El servidor de informes se debe ejecutar en modo nativo. No se puede usar el portal web con un servidor de informes que está configurado para el modo integrado de SharePoint. En SQL Server 2012, no se puede cambiar un servidor de informes de un modo a otro. Si desea cambiar el tipo de servidor de informes que usa su entorno, debe instalar el modo deseado del servidor de informes y, a continuación, copiar o mover los elementos de informe al nuevo servidor de informes. Este proceso se conoce normalmente como 'migración'. Los pasos necesarios para la migración dependen del modo al que se realice la migración y la versión desde la que se migre. Para obtener más información, vea [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

- También debe tener Internet Explorer 11 o posterior con scripting habilitado. Para obtener más información, vea [Compatibilidad del explorador de Reporting Services y Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).

## <a name="configure-the-web-portal-to-use-the-default-url"></a>Configurar el portal web para usar la dirección URL predeterminada

El portal web es una aplicación Web que tienen acceso los usuarios en un explorador Web. Como mínimo, debe definir la dirección URL que se usa para abrir la aplicación en una ventana del explorador. La dirección URL está compuesta de un nombre de host, un puerto y un directorio virtual. Los valores predeterminados para esta dirección URL incluyen el nombre de host y los valores de puerto que definió para el servicio web del servidor de informes, más el nombre del directorio virtual **reports** . Si tiene una instancia con nombre, el directorio virtual es **reports_instance**, donde **instance** es el nombre de la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

De forma predeterminada, el portal web dirección URL se compone de un nombre único de directorio virtual más el nombre de host y un puerto que se define para el servicio Web del servidor de informes que se ejecuta en la misma instancia. En la mayoría de los casos, el nombre de host es el nombre de red del equipo del servidor de informes, pero también puede ser una dirección IP o un encabezado de host que se resuelva como el equipo. Para configurar el portal web para usar la dirección URL predeterminada, use la **dirección URL del Portal Web** página en el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] herramienta de configuración.

> [!TIP]
> Si intenta tener acceso al portal web en un equipo remoto y recibe mensajes de error de conexión en el explorador, una causa común es la configuración del Firewall. Para obtener más información, vea [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).

#### <a name="to-configure-the-default-the-web-portal-url-and-virtual-directory"></a>Para configurar el valor predeterminado el portal web de dirección URL y un directorio virtual

1. Inicie la herramienta Configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y conéctese a la instancia del servidor de informes.

2. En el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] herramienta de configuración, seleccione **dirección URL del Portal Web** para abrir la página para configurar la dirección URL.

3. Escriba un nombre de directorio virtual únicos para el portal web.

4. Haga clic en **Aplicar**.

5. Si utilizas [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] o Windows Server 2008, adicionales pueden ser necesarios pasos antes de poder utilizar el portal web. Para más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).

## <a name="configure-the-web-portal-to-use-a-specific-report-server-url"></a>Configurar el portal web para usar una dirección URL de servidor de informes específico

De forma predeterminada, el portal web le conecta al servicio Web del servidor de informes que se ejecuta en el mismo servicio de servidor de informes. El portal web usa la dirección URL del servicio Web del servidor de informes para realizar la conexión. Si define varias direcciones URL para el servicio Web del servidor de informes, el portal web usa la última de ellas. Sin embargo, en algunas implementaciones, conviene el portal web siempre se conecte al servicio Web a través de una dirección URL estática. Podría interesarle esto si, por ejemplo, hubiese configurado el filtrado de paquetes en un puerto o en una dirección IP específica y deseara que todas las conexiones al servidor de informes pasaran a través de las reglas del filtro que ha definido.

Al configurar las direcciones URL en el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] herramienta de configuración, el portal web detecta y usa automáticamente las direcciones URL nuevas y actualizadas para el servidor de informes que se ejecuta en la misma instancia de servidor. Si su implementación requiere el uso de una única dirección URL estática para todas las solicitudes del servidor de informes, puede especificar dicha dirección en el archivo RSReportServer.config.

#### <a name="to-configure-a-static-report-server-url"></a>Para configurar una dirección URL estática del servidor de informes

1. Abra el archivo **RsReportServer.config** en un editor de texto. De forma predeterminada, se encuentra en \Program SQL Server\MSRS12. \< *nombreDeInstancia*> \Reporting.  

2. Busque **ReportServerURL**.

3. Reemplácelo por la dirección URL de la instancia del servidor de informes.

4. Guarde los cambios y cierre el archivo.

Para obtener más información sobre el archivo de configuración, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md) y [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).

## <a name="customize-styles-or-application-title"></a>Personalizar estilos o el título de la aplicación

Puede crear un paquete de marca personalizada para modificar los colores utilizados para el portal web. Para obtener más información, vea [personalización de marca del portal web](../branding-the-web-portal.md)

#### <a name="to-modify-application-title"></a>Para modificar el título de la aplicación

1. Inicie la sesión usando una cuenta que tenga asignados los permisos **Administrador del sistema** en el servidor de informes.

2. Abra Internet Explorer.

3. Escriba el portal web de dirección URL. De forma predeterminada, es http://\<**el nombre del servidor**> / reports, pero si instaló Reporting Services como una instancia con nombre, la dirección URL predeterminada será http://\<**el nombre del servidor**> / reports\<**_instancename**>.

4. Seleccione **Configuración del sitio**.

5. En la pestaña **General** , en **Nombre**, reemplace **SQL Server Reporting Services** por otro nombre.

6. Seleccione **Aplicar**.

## <a name="next-steps"></a>Pasos siguientes

[Portal Web](../../reporting-services/web-portal-ssrs-native-mode.md)  
[Compatibilidad del explorador de Reporting Services](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)
[configurar una dirección URL](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
[Comprobar una instalación de Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)   
[Activar o desactivar los informes de características de servicios](../../reporting-services/report-server/turn-reporting-services-features-on-or-off.md)   
[Administrar un servidor de informes en modo nativo de Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
[El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[Configurar un servidor de informes de modo nativo para la administración Local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)

 ¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
