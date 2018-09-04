---
title: Direcciones URL en archivos de configuración (Administrador de configuración de SSRS) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fc31fa09432f2710e21eb3328610eb8f0af15c5d
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43269094"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>Direcciones URL en archivos de configuración (Administrador de configuración de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena la configuración de las aplicaciones en un archivo RSReportServer.config. Dentro de este archivo, hay valores de configuración tanto de direcciones URL como de reservas de direcciones URL. Estos valores de configuración tienen propósitos muy diferentes y reglas de modificación. Si está acostumbrado a modificar los archivos de configuración para mejorar una implementación, este tema puede ayudarle a entender cómo se utiliza cada valor de las direcciones URL.  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>Configuración de direcciones URL en el archivo RSReportServer.config  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] almacena direcciones URL para el acceso a informes y aplicaciones, y para conectar los componentes web front-end a un servidor de informes back-end.  
  
#### <a name="urls-for-application-access"></a>Direcciones URL para el acceso de las aplicaciones  
 las direcciones URL se usan para acceder al servicio web del servidor de informes y a [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Para configurar las direcciones URL, debe usar la herramienta Configuración de Reporting Services. La herramienta crea reservas de direcciones URL para cada aplicación en HTTP.SYS y agrega entradas para las direcciones URL en la sección **URLReservations** de RSReportServer.config.  
  
-   Para ver descripciones de cada elemento de la sección **URLReservations** , vea [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para más información sobre la sintaxis del elemento **UrlString**, vea [Sintaxis de reserva de direcciones URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md).  
  
-   Para obtener instrucciones sobre cómo configurar las direcciones URL para el acceso a aplicaciones, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
#### <a name="urls-for-report-access"></a>Direcciones URL para el acceso de los informes  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye una extensión de entrega de correo electrónico del servidor de informes que puede usar para enviar vínculos o datos adjuntos de informes. Un vínculo de informe se construye cuando se entrega el informe. La extensión de entrega de correo electrónico del servidor de informes usa el valor de **UrlRoot** del archivo de configuración para crear el vínculo. **UrlRoot** se usa también para resolver los vínculos de un informe representado que se genera mediante el procesamiento de informes desatendido.  
  
 **UrlRoot** se especifica en el archivo RSReportServer.config automáticamente al configurar direcciones URL para el acceso de las aplicaciones. Si modifica este valor en el archivo de configuración, debe especificar una dirección URL válida para un servicio web del servidor de informes que esté conectado a una base de datos del servidor de informes que contenga los informes que desea entregar. Solo puede especificar una **UrlRoot** para una única instancia del servidor de informes; solo puede existir una entrada **UrlRoot** en el archivo RSReportServer.config para una instancia del servidor de informes determinada. Si tiene varias direcciones URL reservadas para el servicio web del servidor de informes, debe elegir uno de los valores disponibles de **UrlRoot**.  
  
 En la mayor parte de los casos, no necesita modificar **UrlRoot**. Pero si se va a acceder al servidor de informes a través de una dirección URL completa, y no configuró ninguna dirección URL que use un encabezado de host para el nombre del sitio completo, debe modificar manualmente el archivo RSReportServer.config para establecer **UrlRoot** en la dirección URL completa del servidor de informes que se usará para representar el informe (por ejemplo, https://www.adventure-works.com/mywebapp/reportserver).  
  
#### <a name="urls-connecting-the-includessrswebportalincludesssrswebportalmd-and-web-parts-to-the-report-server-web-service"></a>Direcciones URL que conectan el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y los elementos web al servicio web del servidor de informes  
 el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y los elementos web de SharePoint 2.0 para Reporting Services son los componentes web front-end que conectan con un servidor de informes. Entre las direcciones URL que se usan para conectar con un servidor de informes back-end se incluyen las siguientes:  
  
-   **ReportServerUrl** (usado por el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)])  
  
-   **ReportServerExternalUrl** (usado por los elementos web)  
  
> [!NOTE]  
>  Las versiones anteriores de Reporting Services incluían el elemento **ReportServerVirtualDirectory** . Este valor es obsoleto en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. Si actualizó una instalación existente y usa un archivo de configuración que contiene este valor, el servidor de informes ya no lee este valor.  
  
 En la tabla siguiente se proporciona un resumen de todas las direcciones URL que se pueden especificar en un archivo de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Configuración|Uso|Descripción|  
|-------------|-----------|-----------------|  
|**ReportServerUrl**|Opcional. Este elemento no está incluido en el archivo RSReportServer.config a menos que lo agregue usted.<br /><br /> Establezca este elemento solo si está configurando uno de los escenarios siguientes:<br /><br /> el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] proporciona acceso web front-end a un servicio web del servidor de informes que se ejecuta en un equipo diferente o en una instancia diferente en el mismo equipo.<br /><br /> Si tiene varias direcciones URL para un servidor de informes y quiere que el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] use una en concreto.<br /><br /> Tiene una dirección URL concreta del servidor de informes que quiere que se use en todas las conexiones del [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] .<br /><br /> Por ejemplo, podría habilitar el acceso al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] para todos los equipos de la red, y seguir requiriendo que el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] se conecte al servidor de informes a través de una conexión local. En este caso, podría configurar **ReportServerUrl** en "`http://localhost/reportserver`".|Este valor especifica una dirección URL para el servicio web del servidor de informes. La aplicación [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] lee este valor en el inicio. Si se establece este valor, el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] se conectará al servidor de informes que se especifique en la dirección URL.<br /><br /> De forma predeterminada, el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] proporciona acceso web front-end a un servicio web del servidor de informes que se ejecuta dentro de la misma instancia del servidor de informes que el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]. Pero si quiere usar el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] con un servicio web del servidor de informes que forme parte de otra instancia o se ejecute en una instancia de un equipo diferente, puede establecer esta dirección URL para indicar al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] que se conecte al servicio web del servidor de informes externo.<br /><br /> Si en el servidor de informes al que se está conectando hay instalado un certificado de Capa de sockets seguros (SSL), el valor de **ReportServerUrl** debe ser el nombre del servidor que esté registrado para ese certificado. Si se produce un error similar a "Se ha terminado la conexión: no se puede establecer una relación de confianza para el canal seguro SSL/TLS", establezca **ReportServerUrl** en el nombre de dominio completo del servidor para el que se ha emitido el certificado SSL. Por ejemplo, si el certificado está registrado en **https://adventure-works.com.onlinesales**, la dirección URL del servidor de informes sería **https://adventure-works.com.onlinesales/reportserver**.|  
|**ReportServerExternalUrl**|Opcional. Este elemento no está incluido en el archivo RSReportServer.config a menos que lo agregue usted.<br /><br /> Establezca este elemento solo si está utilizando los elementos web de SharePoint 2.0 y desea que los usuarios puedan recuperar un informe y abrirlo en otra ventana del explorador.<br /><br /> Agregue \<**ReportServerExternalUrl**> debajo del elemento \<**ReportServerUrl**> y, luego, establézcalo en un nombre del servidor de informes completo que se resuelva como una instancia del servidor de informes cuando se obtenga acceso a ella en una ventana del explorador independiente. No elimine \<**ReportServerUrl**>.<br /><br /> El siguiente ejemplo ilustra la sintaxis:<br /><br /> `<ReportServerExternalUrl>http://myserver/reportserver</ReportServerExternalUrl>`|Los elementos web de SharePoint 2.0 utilizan este valor.<br /><br /> En versiones anteriores, se recomendaba que estableciera este valor para implementar el Generador de informes en un servidor de informes expuesto a Internet. Este escenario de implementación no se ha probado. Si antes utilizaba este valor para que se admitiera el acceso a través de Internet al Generador de informes, debe considerar la posibilidad de utilizar una estrategia alternativa.|  
  
## <a name="see-also"></a>Ver también  
 [Configurar las direcciones URL del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)
