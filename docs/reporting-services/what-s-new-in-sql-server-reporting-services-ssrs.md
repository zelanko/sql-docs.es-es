---
title: Novedades de Reporting Services (SSRS) | Microsoft Docs
ms.date: 09/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b72f5bfef28c5f434cff07b2a931519c3fefd295
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52712412"
---
# <a name="whats-new-in-sql-server-reporting-services-ssrs"></a>Novedades de SQL Server Reporting Services (SSRS)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)]

Obtenga información sobre las novedades de SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Abarca las principales áreas de características y se actualiza a medida que se lanzan nuevos elementos.

Para ver las notas de la versión actual, consulte [Notas de la versión de SQL Server 2017](../sql-server/sql-server-2017-release-notes.md). 

Para obtener información sobre Power BI Report Server, vea [¿Qué es Power BI Report Server?](https://docs.microsoft.com/power-bi/report-server/get-started).

**Descarga** ![download](../analysis-services/media/download.png "download")

Para descargar SQL Server 2017 Reporting Services, vaya al **[Centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=55252)**.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="sql-server-2019-preview-reporting-services"></a>Versión preliminar de SQL Server 2019 Reporting Services

[!INCLUDE[sql-server-2019]](../includes/sssqlv15-md.md)] Reporting Services no está disponible para CTP 2.1. Instale la versión actual: [SQL Server 2017 Reporting Services](install-windows/install-reporting-services.md).
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
## <a name="ssrs-2017"></a>SSRS 2017

### <a name="comments-on-reports"></a>Comentarios en los informes

Ahora hay comentarios disponibles para los informes a fin de agregar perspectivas y colaborar con otros usuarios. También puede incluir archivos adjuntos con los comentarios.

![Comentarios dentro de un servidor de informes](media/what-s-new-in-sql-server-reporting-services-ssrs/report-server-comments.png)

Para más información, vea [Agregar comentarios a un informe en un servidor de informes](https://powerbi.microsoft.com/documentation/reportserver-add-comments/).

### <a name="dax-queries-in-reporting-tools"></a>Consultas DAX en herramientas de informes

En las versiones más recientes del Generador de informes y SQL Server Data Tools, puede crear consultas DAX nativas sobre los modelos de datos tabulares de SQL Server Analysis Services si arrastra y coloca los campos deseados en los diseñadores de consultas. Consulte el [blog de Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).

### <a name="rest-api-support"></a>Compatibilidad con la API de REST

Para habilitar el desarrollo y personalización de aplicaciones modernas, SQL Server Reporting Services admite ahora una API de RESTful totalmente compatible con OpenAPI. La especificación y la documentación completas de la API se pueden encontrar en [swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0).

### <a name="query-designer-support-for-dax-now-in-report-builder-and-sql-server-data-tools"></a>Compatibilidad con el diseñador de consultas para DAX ahora en el Generador de informes y SQL Server Data Tools

En el Generador de informes y SQL Server Data Tools, ahora se pueden crear consultas DAX nativas sobre los modelos de datos tabulares de SQL Server Analysis Services admitidos. Se puede usar el diseñador de consultas en ambas herramientas para arrastrar y colocar los campos que quiera y hacer que la consulta DAX se genere automáticamente en lugar de escribirla usted mismo.  
 
Lea más en el [blog de Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).

* Descargue [Generador de informes de SQL Server](https://go.microsoft.com/fwlink/?LinkId=734968).
* Descargue [SQL Server Data Tools (versión candidata para lanzamiento)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate).

> **Nota**: Solo se puede usar el diseñador de consultas de DAX con orígenes de datos tabulares de SSAS integrados en SQL Server 2016+.
::: moniker-end
 
## <a name="ssrs-2016"></a>SSRS 2016
  
### <a name="reporting-services-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  
 Un nuevo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] está disponible. Se trata de un portal actualizado y moderno que incorpora KPI, informes móviles, informes paginados y archivos de Excel y Power BI Desktop. El [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] reemplaza al Administrador de informes de versiones anteriores. También puede descargar el Publicador de informes móviles y el Generador de informes desde el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] , sin que sea necesario usar la tecnología ClickOnce.
 
 Para crear informes móviles, necesitará el [!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short.md)].  
  
 Para más información sobre el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)], consulte [Portal web (modo nativo de SSRS)](../reporting-services/web-portal-ssrs-native-mode.md).  
  
 ![ssRSPortal](../reporting-services/media/ssrsportal.png "ssRSPortal")  
 
 #### <a name="custom-branding-for-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Personalización de marca para el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 
  Puede personalizar el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] con el logotipo y los colores de su organización con un paquete de personalización de marca.  
  
  Para más información sobre la personalización de marca, consulte [Personalización de marca del portal web](https://msdn.microsoft.com/6dac97f7-02a6-4711-81a3-e850a6b40bf1).
 
 #### <a name="key-performance-indicators-kpi-in-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Indicadores de rendimiento clave (KPI) en el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 

Puede crear KPI directo en el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] que sean contextuales a la carpeta en que se encuentra. Al crear los KPI, puede elegir campos de conjunto de datos y resumir esos valores. También puede seleccionar contenido relacionado para la obtención de detalles.
  
 ![ssrs-webportal-kpi](../reporting-services/media/ssrs-webportal-kpi.png)
 
 Para más información, vea [Uso de los KPI en Reporting Services](https://msdn.microsoft.com/a28cf500-6d47-4268-a248-04837e7a09eb)
  
 
 ### <a name="mobile-reports"></a>Mobile Reports (Informes móviles)
 
Los informes móviles de Reporting Services son informes dedicados optimizados para una amplia variedad de factores de forma y para ofrecer una experiencia óptima para usuarios que accedan a informes en dispositivos móviles. Los informes móviles cuentan con una amplia variedad de visualizaciones, desde gráficos de tiempo, categoría y comparación, hasta gráficos de rectángulos y mapas personalizados. Puede conectar sus informes móviles a una gran variedad de orígenes de datos, como datos tabulares y multidimensionales de SQL Server Analysis Services local. Cree informes móviles en una superficie de diseño con cuadrícula ajustable de filas y columnas, y elementos flexibles de informes móviles que se escalan correctamente para cualquier tamaño de pantalla. Después, guarde estos informes móviles en un servidor de Reporting Services y visualice e interactúe con estos en un explorador o en la aplicación móvil de Power BI en dispositivos iPad, iPhone, Android y Windows 10.
  
#### <a name="mobile-report-publisher"></a>Publicador de informes móviles  
 El [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long.md)]le permite crear y publicar informes móviles de SQL Server en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)].  
  
 ![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "SS_MRP_LayoutTabSmall")  
  
 Para más información, vea [Creación y publicación de informes móviles con el Publicador de informes móviles de SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).  
  
#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>Informes móviles de SQL Server hospedados en Reporting Services disponibles en la aplicación móvil de Power BI  
 La aplicación móvil de Power BI para iOS en iPad y iPhone puede mostrar ahora informes móviles de SQL Server hospedados en el servidor de informes local.  
  
 ![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "SS_MRP_iPad_HomeSm")  
  
 No puede conectarse de forma predeterminada sin realizar algunos cambios en la configuración. Para obtener más información sobre cómo permitir que la aplicación móvil de Power BI se conecte a su servidor de informes, consulte [Habilitar un servidor de informes para el acceso mediante móvil a Power BI](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md).
  
### <a name="support-of-sharepoint-mode-and-sharepoint-2016"></a>Compatibilidad del modo de SharePoint y SharePoint 2016  
 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite la integración con SharePoint 2013 y SharePoint 2016.
 
Para obtener más información, vea:  
  
-   [Combinaciones admitidas del servidor y el complemento de SharePoint y Reporting Services &#40;SQL Server 2016&#41;](../reporting-services/install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
-   [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Instalar el modo de SharePoint de Reporting Services](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md)  

### <a name="microsoft-net-framework-4-support"></a>Compatibilidad con Microsoft .NET Framework 4  
 [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] admite las versiones actuales de Microsoft .NET Framework 4. Esto incluye la versión 4.0 y 4.5.1. Si no hay instalada ninguna versión de .NET Framework 4.x, la configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalará .NET 4.0 durante el paso de instalación de las características.  

### <a name="report-improvements"></a>Mejoras del informe

**Motor de representación HTML 5:** un nuevo motor de representación HTML5 destinado al modo de estándares modernos web "completos" y a los exploradores modernos.  El nuevo motor de representación ya no cuenta con el modo de interpretación usado por algunos exploradores antiguos.
  
 Para más información sobre la compatibilidad de exploradores, vea [Compatibilidad del explorador de Reporting Services y Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).  

**Informes paginados modernos** : diseñe informes paginados modernos y muy atractivos con nuevos estilos modernos para gráficos, medidores, mapas y otras visualizaciones de datos.
  
**Gráficos de rectángulos y proyección solar:** mejore sus informes con gráficos de rectángulos ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") y proyección solar ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon"), formas estupendas para mostrar datos jerárquicos. Para obtener más información, consulte [Tree Map and Sunburst Charts in Reporting Services](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md).  

**Inserción de informes:** ahora puede insertar informes paginados o móviles en otras páginas web y aplicaciones; para ello, puede usar un iframe junto con los parámetros de dirección URL.  

**Anclar elementos de informe a un panel de Power BI:** mientras se visualiza un informe en el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], puede seleccionar elementos de informe y anclarlos a un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .   Puede anclar elementos como gráficos, paneles de medidores, mapas e imágenes. Puede **(1)** seleccionar el grupo que contiene el panel que quiere anclar, **(2)** seleccionar el panel donde también quiere anclar el elemento y **(3)** seleccionar la frecuencia con la que quiere que se actualice el icono en el panel.   ![nota](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "nota") Las suscripciones de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] administran la actualización y, después de anclar el elemento, se pueden modificar para configurar una programación de actualización distinta.  
  
 ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png) 
  
 Para más información, vea [Integración de Power BI Report Server &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md) y [Anclado de elementos de Reporting Services en paneles de Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).  
 
 **Representación y exportación de PowerPoint:** el formato PPTX (Microsoft PowerPoint) es una nueva extensión de representación de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] . Puede exportar informes en formato PPTX desde las aplicaciones habituales, como el Generador de informes, el Diseñador de informes (en SSDT) y el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. A modo de ejemplo, en la imagen siguiente se muestra el menú Exportar en [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. 
  
 ![ssrs-export-powerpoint](../reporting-services/media/ssrs-export-powerpoint.png) 
  
 También puede seleccionar el formato PPTX para la salida de la suscripción y usar el acceso de dirección URL del servidor de informes para representar y exportar un informe. Por ejemplo, el siguiente comando de dirección URL de su explorador exporta un informe desde una instancia con nombre del servidor de informes.  
  
```  
https://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
```  
  
 Para obtener más información, consulte [Export a Report Using URL Access](../reporting-services/export-a-report-using-url-access.md).  
 
 **PDF reemplaza a ActiveX para la impresión remota:** la experiencia de impresión ActiveX de la barra de herramientas del visor de informes se ha reemplazado por una experiencia moderna basada en PDF que funciona en la matriz de exploradores admitidos, como Microsoft Edge. No necesita descargar más controles de ActiveX. Según el explorador que use y las aplicaciones y servicios de visualización de PDF que haya instalado, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] abrirá un diálogo de impresión para imprimir el informe o le pedirá que descargue un archivo .PDF del informe.  Como administrador, puede deshabilitar la impresión del lado del cliente desde [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]. Para más información, vea [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).

![ssrs-pdf-printing](../reporting-services/media/ssrs-pdf-printing.png)

### <a name="subscription-improvements"></a>Mejoras en la suscripción  
 
|Característica|Modo de servidor admitido|  
|-------------|---------------------------|  
|**Habilitar y deshabilitar suscripciones**. Hay opciones nuevas de interfaz de usuario para habilitar y deshabilitar rápidamente las suscripciones. Las suscripciones deshabilitadas mantienen sus otras propiedades de configuración, como la programación, y pueden habilitarse fácilmente.<br /><br /> ![ssrs-enable-disable-subscriptions](../reporting-services/media/ssrs-enable-disable-subscriptions.png)<br /><br /> Para obtener más información, consulte [Disable or Pause Report and Subscription Processing](../reporting-services/subscriptions/disable-or-pause-report-and-subscription-processing.md).|en modo nativo|  
|**Descripción de la suscripción**. Cuando crea una nueva suscripción, ahora puede incluir una descripción del informe como parte de las propiedades de la suscripción. La descripción se incluye en la página de resumen de la suscripción.|Modo nativo y SharePoint|  
|**Cambiar el propietario de la suscripción**. Se ha mejorado la interfaz de usuario para poder cambiar rápidamente el propietario de una suscripción. Las versiones anteriores de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] permiten a los administradores cambiar los propietarios de la suscripción con un script. A partir de la versión de [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] , puede cambiar los propietarios de la suscripción con la interfaz de usuario o con un script. El cambio del propietario de una suscripción es una tarea administrativa común cuando los usuarios dejan la organización o cuando cambian sus roles.|Modo nativo y SharePoint|  
|**Credenciales compartidas para las suscripciones de recurso compartido de archivos**. Ahora existen dos flujos de trabajo con las suscripciones de recurso compartido de archivos de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :<br /><br /> Como novedad de esta versión, el administrador de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] puede configurar una única cuenta de recurso compartido de archivos, que se usa para una o para varias suscripciones. Para configurar la cuenta de recurso compartido de archivos, el administrador de configuración del modo nativo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] debe definir la opción **Specify a file share account**(Especificar una cuenta de recurso compartido de archivos) y, después, en la página de configuración de la suscripción, los usuarios deben seleccionar **Use file share account**(Usar la cuenta de recurso compartido de archivos).<br /><br /> Configure suscripciones individuales con credenciales específicas para el recurso compartido de archivos de destino.<br /><br /> También puede combinar los dos enfoques y definir que algunas suscripciones de recurso compartido de archivos usen la cuenta central de recurso compartido de archivos mientras otras suscripciones usan credenciales específicas.|en modo nativo|  

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
 En la nueva versión de SSDT se incluyen plantillas de proyecto para [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]: Asistente de proyectos de servidor de informes y Proyecto de servidor de informes. Para obtener más información acerca de la descarga de SSDT, consulte [SQL Server Data Tools para Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=827542).  

### <a name="report-builder-improvements"></a>Mejoras del generador de informes

**Nueva interfaz de usuario del Generador de informes:** la interfaz de usuario principal de [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] ahora tiene una apariencia moderna, con elementos de interfaz de usuario simplificados.  
  
|||  
|-|-|  
|Nuevo|Previous|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "ssrs_rbfacelift_new")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "ssrs_rbfacelift_old")|  

**Panel de parámetros personalizado:** ahora puede personalizar el panel de parámetros. Al usar la superficie de diseño en el Generador de informes, puede arrastrar un parámetro a una columna y una fila específica en el panel de parámetros. Puede agregar y quitar columnas para cambiar el diseño del panel.   Para más información, vea [Customize the Parameters Pane in a Report &#40;Report Builder&#41; (Personalizar el panel de parámetros en un informe [Generador de informes])](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md).  
  
 ![Lista de parámetros en el panel Datos de informe y en el panel Parámetros](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "Lista de parámetros en el panel Datos de informe y en el panel Parámetros")  

  
**Compatibilidad con configuración elevada de ppp:** [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)] es compatible con el escalado y los dispositivos con valores altos de PPP (puntos por pulgada).  Para obtener más información sobre los valores altos de PPP, consulte los artículos siguientes:  
  
-   [Windows 8.1 DPI Scaling Enhancements (Mejoras en el ajuste de escala de PPP en Windows 8.1)](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  
  
-   [Valores altos de PPP y Windows 8.1](https://technet.microsoft.com/library/dn528848.aspx)  

## <a name="next-steps"></a>Pasos siguientes

[Novedades de Analysis Services](https://msdn.microsoft.com/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
[Compatibilidad con versiones anteriores](reporting-services-backward-compatibility.md)   
[Características de Reporting Services compatibles con las ediciones de SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)   
[Actualizar y migrar Reporting Services](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
