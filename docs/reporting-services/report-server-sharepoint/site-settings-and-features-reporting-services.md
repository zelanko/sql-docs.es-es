---
title: "Configuración del sitio y las características del sitio (modo de SharePoint) de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 044346bd4532c691861689662edbcbb37812b7ff
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="site-settings-and-features---reporting-services"></a>Configuración del sitio y características - Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tiene varias características personalizadas de nivel de sitio y una característica de sitio que se pueden administrar desde la página de configuración del sitio de SharePoint. Los valores de configuración se aplican a todo el sitio y afectan a todas las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Debe tener permisos de Administrador de contenido y Administrador del sistema para ver esta página.  
  
|Configuración del sitio|Description|  
|------------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuración del sitio|En este tema se describe la configuración de todo el sitio.|  
|Administrar alertas de datos|Característica de administración de alertas de datos.|  
|Sincronización de archivos del Servidor de informes|Característica de nivel de sitio que está desactivada de forma predeterminada.<br /><br /> Sincroniza los archivos del servidor de informes (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) entre una biblioteca de documentos de SharePoint y el servidor de informes si los archivos se agregan o se actualizan directamente en la biblioteca de documentos.<br /><br /> Para obtener más información, consulte [Activate the Report Server File Sync Feature in SharePoint Central Administration](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>Para abrir la página Configuración del sitio de Reporting Services  
  
1.  En el menú **Acciones del sitio** del sitio de SharePoint, haga clic en **Configuración del sitio**.  
  
2.  En la sección **Reporting Services** , haga clic en **Configuración del sitio de Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opciones de configuración del sitio de Reporting Services  
  
|Opción|Description|  
|------------|-----------------|  
|**Habilitar la descarga del control ActiveX de RSClientPrint**|El control muestra un cuadro de diálogo de impresión personalizado compatible con características comunes a otros cuadros de diálogo de impresión, incluida la vista previa de impresión, selecciones de páginas para especificar páginas e intervalos de páginas, márgenes y orientación. Para obtener más información acerca del control, vea [Using the RSClientPrint Control in Custom Applications](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar los errores remotos en modo local**|Muestre u oculte mensajes de error detallados en equipos remotos cuando la ejecución se realice en modo local. Si ve un mensaje de error similar al siguiente, es posible que habilitar errores remotos pueda ser de utilidad:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar los metadatos de accesibilidad para los informes**|Activa los metadatos de accesibilidad de la salida HTML en los informes|  
|**Habilitar el tamaño exacto de ajuste de visualización de datos en los informes**|Configure el comportamiento de ajuste para la visualización de datos cuando esté en un Tablix, para corregir con exactitud. Esto incluye un gráfico, un medidor y un mapa. Cuando se deshabilita el comportamiento, se hace para que las visualizaciones de datos se ajusten aproximadamente, lo cual podría dejar algún espacio vacío. Este valor de configuración solo se aplica a las representaciones del elemento web del visor de informes. Para administrar este comportamiento en la representación del lado servidor, debe modificar el archivo **rsreportserver.config** . Para obtener más información, vea:<br /><br /> [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Customize Rendering Extension Parameters in RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md).<br /><br /> Si se habilita Exacto, podría repercutir en el rendimiento porque el procesamiento para determinar el tamaño exacto puede conllevar más tiempo que un ajuste aproximado.|  
  
## <a name="see-also"></a>Vea también  
 [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
