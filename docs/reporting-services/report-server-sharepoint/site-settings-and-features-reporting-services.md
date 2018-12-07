---
title: Valores de configuración del sitio de Reporting Services y características del sitio (modo de SharePoint) | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 10e04d4864ac3f6ecf7c59f989a8886cee2409d5
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52414782"
---
# <a name="reporting-services-site-settings-and-site-features-sharepoint-mode"></a>Valores de configuración del sitio de Reporting Services y características del sitio (modo de SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

El modo de SharePoint de Reporting Services tiene varias características personalizadas de nivel de sitio y una característica de sitio que se pueden administrar desde la página de configuración del sitio de SharePoint. La configuración se aplica a todo el sitio y afecta a todas las aplicaciones de servicio de Reporting Services. Debe tener permisos de Administrador de contenido y Administrador del sistema para ver esta página.  

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

|Configuración del sitio|Descripción|  
|------------------|-----------------|  
|Configuración del sitio de Reporting Services|En este tema se describe la configuración de todo el sitio.|  
|Administrar alertas de datos|Característica de administración de alertas de datos.|  
|Sincronización de archivos del Servidor de informes|Característica de nivel de sitio que está desactivada de forma predeterminada.<br /><br /> Sincroniza los archivos del servidor de informes (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) entre una biblioteca de documentos de SharePoint y el servidor de informes si los archivos se agregan o se actualizan directamente en la biblioteca de documentos.<br /><br /> Para obtener más información, consulte [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md).|  
  
## <a name="open-the-reporting-services-site-settings-page"></a>Abra la página Configuración del sitio de Reporting Services
  
1.  En el menú **Acciones del sitio** del sitio de SharePoint, seleccione **Configuración del sitio**.  
  
2.  En la sección **Reporting Services**, seleccione **Configuración del sitio de Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opciones de configuración del sitio de Reporting Services
  
|Opción|Descripción|  
|------------|-----------------|  
|**Habilitar la descarga del control ActiveX de RSClientPrint**|El control muestra un cuadro de diálogo de impresión personalizado compatible con características comunes a otros cuadros de diálogo de impresión, incluida la vista previa de impresión, selecciones de páginas para especificar páginas e intervalos de páginas, márgenes y orientación. Para obtener más información acerca del control, vea [Using the RSClientPrint Control in Custom Applications](../../reporting-services/report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar los errores remotos en modo local**|Muestre u oculte mensajes de error detallados en equipos remotos cuando la ejecución se realice en modo local. Si ve un mensaje de error similar al siguiente, es posible que habilitar errores remotos pueda ser de utilidad:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar los metadatos de accesibilidad para los informes**|Activa los metadatos de accesibilidad de la salida HTML en los informes|  
|**Habilitar el tamaño exacto de ajuste de visualización de datos en los informes**|Configure el comportamiento de ajuste para la visualización de datos cuando esté en un Tablix, para corregir con exactitud. Esto incluye un gráfico, un medidor y un mapa. Cuando se deshabilita el comportamiento, se hace para que las visualizaciones de datos se ajusten aproximadamente, lo cual podría dejar algún espacio vacío. Este valor de configuración solo se aplica a las representaciones en el elemento web Visor de informes. Para administrar este comportamiento en la representación del lado servidor, debe modificar el archivo **rsreportserver.config**. Para obtener más información, vea:<br /><br /> [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Customize Rendering Extension Parameters in RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md).<br /><br /> Si se habilita Exacto, podría repercutir en el rendimiento porque el procesamiento para determinar el tamaño exacto puede conllevar más tiempo que un ajuste aproximado.|  
  
## <a name="see-also"></a>Vea también

 [Administración de una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
