---
title: Reporting Services configuración del sitio y características del sitio (modo de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e0040fec-e2b7-4099-ae01-3b9bb9128bbd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eb2544db775987ff44e54b10163812ac53620a9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102797"
---
# <a name="reporting-services-site-settings-and-site-featuressharepoint-mode"></a>Valores de configuración del sitio de Reporting Services y características del sitio (modo de SharePoint)
  
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tiene varias características personalizadas de nivel de sitio y una característica de sitio que se pueden administrar desde la página de configuración del sitio de SharePoint. Los valores de configuración se aplican a todo el sitio y afectan a todas las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Debe tener permisos de Administrador de contenido y Administrador del sistema para ver esta página.  
  
|Configuración del sitio|Descripción|  
|------------------|-----------------|  
|
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Configuración del sitio|En este tema se describe la configuración de todo el sitio.|  
|Administrar alertas de datos|Característica de administración de alertas de datos.|  
|Sincronización de archivos del Servidor de informes|Característica de nivel de sitio que está desactivada de forma predeterminada.<br /><br /> Sincroniza los archivos del servidor de informes (.rdl, .rsds, .smdl, .rsd, .rsc, .rdlx) entre una biblioteca de documentos de SharePoint y el servidor de informes si los archivos se agregan o se actualizan directamente en la biblioteca de documentos.<br /><br /> Para obtener más información, consulte [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md).|  
  
## <a name="to-open-the-reporting-services-site-settings-page"></a>Para abrir la página Configuración del sitio de Reporting Services  
  
1.  En el menú acciones del **sitio** del sitio de SharePoint, haga clic en **configuración del sitio**.  
  
2.  En la sección **Reporting Services** , haga clic en **Configuración del sitio de Reporting Services**.  
  
## <a name="options-for-reporting-services-site-settings"></a>Opciones de configuración del sitio de Reporting Services  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Habilitar la descarga del control ActiveX de RSClientPrint**|El control muestra un cuadro de diálogo de impresión personalizado compatible con características comunes a otros cuadros de diálogo de impresión, incluida la vista previa de impresión, selecciones de páginas para especificar páginas e intervalos de páginas, márgenes y orientación. Para obtener más información acerca del control, vea [Using the RSClientPrint Control in Custom Applications](report-server-web-service/net-framework/using-the-rsclientprint-control-in-custom-applications.md)|  
|**Habilitar errores remotos en modo local**|Muestre u oculte mensajes de error detallados en equipos remotos cuando la ejecución se realice en modo local. Si ve un mensaje de error similar al siguiente, es posible que habilitar errores remotos pueda ser de utilidad:<br /><br /> `For more information about this error navigate to the report server on the local server machine or enable remote errors`|  
|**Habilitar los metadatos de accesibilidad para los informes**|Activa los metadatos de accesibilidad de la salida HTML en los informes|  
|**Habilitar ajuste de tamaño exacto de visualización de datos para informes**|Configure el comportamiento de ajuste para la visualización de datos cuando esté en un Tablix, para corregir con exactitud. Esto incluye un gráfico, un medidor y un mapa. Cuando se deshabilita el comportamiento, se hace para que las visualizaciones de datos se ajusten aproximadamente, lo cual podría dejar algún espacio vacío. Este valor de configuración solo se aplica a las representaciones del elemento web del visor de informes. Para administrar este comportamiento en la representación del lado servidor, debe modificar el archivo **rsreportserver.config** . Para obtener más información, vea lo siguiente:<br /><br /> [Archivo de configuración RSReportServer](report-server/rsreportserver-config-configuration-file.md).<br /><br /> [Personalizar los parámetros de extensión de representación en Rsreportserver. config](customize-rendering-extension-parameters-in-rsreportserver-config.md).<br /><br /> [Configuración de la información del dispositivo HTML](html-device-information-settings.md).<br /><br /> Si se habilita Exacto, podría repercutir en el rendimiento porque el procesamiento para determinar el tamaño exacto puede conllevar más tiempo que un ajuste aproximado.|  
  
## <a name="see-also"></a>Consulte también  
 [Administrar una aplicación de servicio de SharePoint de Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
  
