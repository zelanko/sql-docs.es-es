---
title: Novedades de Reporting Services (SSRS) | Documentos de Microsoft
ms.date: 07/02/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- what's new [Reporting Services]
- Reporting Services, what's new
- SQL Server Reporting Services, what's new
- SSRS, what's new
ms.assetid: bc909063-6b84-4b3a-80d2-e93fc04b4b9d
caps.latest.revision: 206
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 3a8ed8433d06f9f0250c42f6e5a190bc64e30235
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="whats-new-in-sql-server-reporting-services-ssrs"></a>Novedades de SQL Server Reporting Services (SSRS)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)]

Obtenga información acerca de cuáles son las novedades en SQL Server [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Abarca las principales áreas de características y se actualiza a medida que se lanzan nuevos elementos.
  
  Para obtener información sobre cuáles son las novedades en otras áreas de SQL Server, vea [What's New en SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md) o [What's New in SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md).
  
 **Descarga** ![download](../analysis-services/media/download.png "download")
 
- Para descargar la versión preliminar técnica de informes de Power BI en SQL Server Reporting Services de enero de 2017, junto con la versión de Power BI Desktop (SQL Server Reporting Services), vaya al **[Centro de descarga de Microsoft](https://go.microsoft.com/fwlink/?linkid=839351)**.
  
-   Para descargar [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], vaya al  **[Centro de evaluación](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
  
-   ¿Tiene una cuenta de Azure?  A continuación, vaya  **[aquí](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016sp1enterprisewindowsserver2016/)**  para poner en marcha una máquina Virtual con SQL Server ya instalado.  

 ![Tenga en cuenta](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Nota") para las notas de la versión actual, vea [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md) o [notas de la versión de servidor de informes de Power BI](https://powerbi.microsoft.com/documentation/reportserver-release-notes/).

Para obtener información sobre el servidor de informes de Power BI, consulte [empezar a trabajar con el servidor de informes de Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

## <a name="query-designer-support-for-dax-now-in-report-builder-and-sql-server-data-tools"></a>Diseñador compatibilidad con consultas de DAX ahora en el generador de informes y las herramientas de datos de SQL Server

En las últimas versiones del generador de informes y SQL Server Data Tools – Release Candidate, ahora puede crear consultas nativas de DAX sobre los modelos de datos tabulares de Analysis Services de SQL Server admitidos. Puede utilizar el Diseñador de consultas en ambas herramientas para arrastrar y colocar los campos que desee y tener la consulta DAX generada automáticamente en lugar de escribir usted mismo.  
 
Leer más sobre la [blog de Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).

* Descargar [generador de informes SQL Server 2016](https://go.microsoft.com/fwlink/?LinkId=734968).
* Descargar [herramientas de datos SQL Server: candidato de versión comercial](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate).

> **Tenga en cuenta**: solo se puede utilizar el Diseñador de consultas de DAX con orígenes de datos tabulares de SSAS integrados en SQL Server 2016 +.
 
## <a name="whats-new-in-sql-server-2016"></a>Novedades de SQL Server 2016
  
### <a name="reporting-services-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Reporting Services [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)]  
 Un nuevo [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] está disponible. Se trata de un portal actualizado y moderno que incorpora KPI, informes móviles, informes paginados y archivos de Excel y Power BI Desktop. El [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] reemplaza al Administrador de informes de versiones anteriores. También puede descargar el Publicador de informes móviles y el Generador de informes desde el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] , sin que sea necesario usar la tecnología ClickOnce.
 
 Para crear informes móviles, necesitará el [!INCLUDE[SS_MobileReptPub_Short](../includes/ss-mobilereptpub-short-md.md)].  
  
 Para más información sobre el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)], consulte [Portal web (modo nativo de SSRS)](../reporting-services/web-portal-ssrs-native-mode.md).  
  
 ![ssRSPortal](../reporting-services/media/ssrsportal.png "ssRSPortal")  
 
 #### <a name="custom-branding-for-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Personalización de marca para el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 
  Puede personalizar el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] con el logotipo y los colores de su organización con un paquete de personalización de marca.  
  
  Para más información sobre la personalización de marca, consulte [Personalización de marca del portal web](http://msdn.microsoft.com/en-us/6dac97f7-02a6-4711-81a3-e850a6b40bf1).
 
 #### <a name="key-performance-indicators-kpi-in-the-includessrswebportal-non-markdownincludesssrswebportal-non-markdown-mdmd"></a>Indicadores de rendimiento clave (KPI) en el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] 

Puede crear KPI directo en el [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)] que sean contextuales a la carpeta en que se encuentra. Al crear los KPI, puede elegir campos de conjunto de datos y resumir esos valores. También puede seleccionar contenido relacionado para la obtención de detalles.
  
 ![ssrs-webportal-kpi](../reporting-services/media/ssrs-webportal-kpi.png)
 
 Para más información, vea [Uso de los KPI en Reporting Services](http://msdn.microsoft.com/en-us/a28cf500-6d47-4268-a248-04837e7a09eb)
  
 
 ### <a name="mobile-reports"></a>Mobile Reports (Informes móviles)
 
Los informes móviles de Reporting Services son informes dedicados optimizados para una amplia variedad de factores de forma y para ofrecer una experiencia óptima para usuarios que accedan a informes en dispositivos móviles. Los informes móviles cuentan con una amplia variedad de visualizaciones, desde gráficos de tiempo, categoría y comparación, hasta gráficos de rectángulos y mapas personalizados. Puede conectar sus informes móviles a una gran variedad de orígenes de datos, como datos tabulares y multidimensionales de SQL Server Analysis Services local. Cree informes móviles en una superficie de diseño con cuadrícula ajustable de filas y columnas, y elementos flexibles de informes móviles que se escalan correctamente para cualquier tamaño de pantalla. Después, guarde estos informes móviles en un servidor de Reporting Services y visualice e interactúe con estos en un explorador o en la aplicación móvil de Power BI en dispositivos iPad, iPhone, Android y Windows 10.
  
#### <a name="mobile-report-publisher"></a>Publicador de informes móviles  
 El [!INCLUDE[SS_MobileReptPub_Long](../includes/ss-mobilereptpub-long-md.md)]le permite crear y publicar informes móviles de SQL Server en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssRSWebPortal-Non-Markdown](../includes/ssrswebportal-non-markdown-md.md)].  
  
 ![SS_MRP_LayoutTabSmall](../reporting-services/media/ss-mrp-layouttabsm.png "SS_MRP_LayoutTabSmall")  
  
 Para más información, vea [Creación y publicación de informes móviles con el Publicador de informes móviles de SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).  
  
#### <a name="sql-server-mobile-reports-hosted-in-reporting-services-available-in-power-bi-mobile-app"></a>Informes móviles de SQL Server hospedados en Reporting Services disponibles en la aplicación móvil de Power BI  
 La aplicación móvil de Power BI para iOS en iPad y iPhone puede mostrar ahora informes móviles de SQL Server hospedados en el servidor de informes local.  
  
 ![SS_MRP_iPad_HomeSm](../reporting-services/media/ss-mrp-ipad-homesm.png "SS_MRP_iPad_HomeSm")  
  
 No puede conectarse de forma predeterminada sin realizar algunos cambios en la configuración. Para obtener más información sobre cómo permitir que la aplicación móvil de Power BI se conecte a su servidor de informes, consulte [Enable a report server for Power BI Mobile access](../reporting-services/report-server/enable-a-report-server-for-power-bi-mobile-access.md).
  
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
  
**Rectángulos y proyección solar gráficos:** Mejore sus informes con rectángulos ![ssrs_treemap_icon](../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon") y proyección solar ![ssrs_sunburst_icon](../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon") gráficos, formas estupendas para mostrar los datos jerárquicos. Para obtener más información, consulte [Tree Map and Sunburst Charts in Reporting Services](../reporting-services/report-design/tree-map-and-sunburst-charts-in-reporting-services.md).  

**Inserción de informes:** ahora puede insertar informes paginados o móviles en otras páginas web y aplicaciones; para ello, puede usar un iframe junto con los parámetros de dirección URL.  

**Anclar elementos de informe a un panel de Power BI:** mientras se visualiza un informe en el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], puede seleccionar elementos de informe y anclarlos a un panel de [!INCLUDE[sspowerbi](../includes/sspowerbi-md.md)] .   Puede anclar elementos como gráficos, paneles de medidores, mapas e imágenes. Puede **(1)** seleccionar el grupo que contiene el panel que quiere anclar, **(2)** seleccionar el panel donde también quiere anclar el elemento y **(3)** seleccionar la frecuencia con la que quiere que se actualice el icono en el panel.   ![Tenga en cuenta](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png "Nota") administra la actualización [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] suscripciones y después de ancla el elemento, puede editar la suscripción y configurar una programación de actualización diferentes.  
  
 ![ssRS_Pin_to_PowerBI](../reporting-services/media/ssrs-pin-to-powerbi.png) 
  
 Para más información, vea [Integración del servidor de informes de Power BI &#40;Configuration Manager&#41;](../reporting-services/install-windows/power-bi-report-server-integration-configuration-manager.md) y [Anclado de elementos de Reporting Services en paneles de Power BI](../reporting-services/pin-reporting-services-items-to-power-bi-dashboards.md).  
 
 **Representación y exportación de PowerPoint:** el formato PPTX (Microsoft PowerPoint) es una nueva extensión de representación de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Puede exportar informes en formato PPTX desde las aplicaciones habituales, como el Generador de informes, el Diseñador de informes (en SSDT) y el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. A modo de ejemplo, en la imagen siguiente se muestra el menú Exportar en [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. 
  
 ![ssrs-export-powerpoint](../reporting-services/media/ssrs-export-powerpoint.png) 
  
 También puede seleccionar el formato PPTX para la salida de la suscripción y usar el acceso de dirección URL del servidor de informes para representar y exportar un informe. Por ejemplo, el siguiente comando de dirección URL de su explorador exporta un informe desde una instancia con nombre del servidor de informes.  
  
```  
http://servername/ReportServer_THESQLINSTANCE/Pages/ReportViewer.aspx?%2freportfolder%2freport+name+with+spaces&rs:Format=pptx  
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
 En la nueva versión de SSDT se incluyen plantillas de proyecto para [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]: Asistente de proyectos de servidor de informes y Proyecto de servidor de informes. Para obtener más información acerca de la descarga de SSDT, consulte [SQL Server Data Tools para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=827542).  

### <a name="report-builder-improvements"></a>Mejoras del generador de informes

**Nueva interfaz de usuario del Generador de informes:** la interfaz de usuario principal de [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] ahora tiene una apariencia moderna, con elementos de interfaz de usuario simplificados.  
  
|||  
|-|-|  
|Nuevo|Previous|  
|![ssrs_rbfacelift_new](../reporting-services/media/ssrs-rbfacelift-new.png "ssrs_rbfacelift_new")|![ssrs_rbfacelift_old](../reporting-services/media/ssrs-rbfacelift-old.png "ssrs_rbfacelift_old")|  

**Panel de parámetros personalizado:** ahora puede personalizar el panel de parámetros. Al usar la superficie de diseño en el Generador de informes, puede arrastrar un parámetro a una columna y una fila específica en el panel de parámetros. Puede agregar y quitar columnas para cambiar el diseño del panel.   Para más información, vea [Customize the Parameters Pane in a Report &#40;Report Builder&#41;](../reporting-services/report-design/customize-the-parameters-pane-in-a-report-report-builder.md) (Personalizar el panel de parámetros en un informe [Generador de informes]).  
  
 ![Lista de parámetros en el panel datos de informe y panel de parámetros](../reporting-services/media/ssrs-customizeparameter-parameterlist-reportdatapane.png "lista de parámetros en el panel datos de informe y panel de parámetros")  

  
**Compatibilidad con alta de PPP:** [!INCLUDE[ssRBnoversion](../includes/ssrbnoversion-md.md)] es compatible con dispositivos y ajuste de escala en los valores altos de PPP (puntos por pulgada).  Para obtener más información sobre los valores altos de PPP, consulte los artículos siguientes:  
  
-   [Windows 8.1 DPI Scaling Enhancements (Mejoras en el ajuste de escala de PPP en Windows 8.1)](https://blogs.windows.com/windowsexperience/2013/07/15/windows-8-1-dpi-scaling-enhancements/)  
  
-   [Valores altos de PPP y Windows 8.1](http://technet.microsoft.com/library/dn528848.aspx)  

## <a name="next-steps"></a>Pasos siguientes

[Novedades de Analysis Services](http://msdn.microsoft.com/en-us/aa69c299-b8f4-4969-86d8-b3292fe13f08)  
[Versión preliminar técnica de informes de Power BI en SSRS: notas de la versión](../reporting-services/reporting-services-release-notes.md)  
[Notas de la versión de SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)   
[Compatibilidad con versiones anteriores](http://msdn.microsoft.com/en-us/675b0e0e-cfee-4790-9675-80fc3ea6d30f)   
[Características de Reporting Services compatibles con las ediciones de SQL Server 2016](http://msdn.microsoft.com/en-us/39f03d2d-6e48-4b34-a9d3-07f86313b937)   
[Actualizar y migrar Reporting Services](../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
[Servidor de informes de BI de energía](https://powerbi.microsoft.com/documentation/reportserver-get-started/)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
