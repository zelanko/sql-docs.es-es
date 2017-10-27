---
title: Reporting Services (SSRS) | Documentos de Microsoft
description: "Obtenga información sobre herramientas y servicios para móviles y paginados informes de Reporting Services e informes de Power BI de forma local."
ms.custom: 
ms.date: 07/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- reports [Reporting Services]
- SSRS
- reports [Reporting Services], about reports
- Reporting Services
- SQL Server Reporting Services
ms.assetid: b8d18d3d-9db0-43e7-8286-7b46cc3a37ed
caps.latest.revision: 70
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Active
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 49f990d30564a2c4fc38a527e7da1e97f9a21ca1
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="what-is-sql-server-reporting-services-ssrs"></a>¿Qué es SQL Server Reporting Services (SSRS)?

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

Crear, implementar y administrar informes paginados o móviles de Reporting Services e informes de Power BI de forma local y el intervalo de listos para usar herramientas y servicios que SQL Server Reporting Services (SSRS) y Power BI proporcionan.

![SQL Server Reporting Services todos juntos](../reporting-services/media/ss-reporting-services-all-together.png "SQL Server Reporting Services todos juntos")

## <a name="create-deploy-and-manage-mobile-and-paginated-reports"></a>Crear, implementar y administrar informes paginados o móviles

SQL Server Reporting Services es una solución que los clientes pueden implementar de forma local para crear, publicar y administrar informes y, luego, entregarlos a los usuarios adecuados de distintas formas: visualizándolos en el explorador web, en el dispositivo móvil o como correo electrónico en su Bandeja de entrada.

Para SQL Server 2016, Reporting Services ofrece un conjunto actualizado de productos:

* **Informes paginados "tradicionales"** actualizados, de modo que pueda crear informes de aspecto moderno, con herramientas actualizadas y nuevas características para crearlos.
* **Nuevos informes móviles** con un diseño con capacidad de respuesta que se adapta a diferentes dispositivos y a las distintas formas en que los sostiene.
* **Un portal web moderno** que puede ver en cualquier explorador moderno. En el nuevo portal, puede organizar y mostrar paginados o móviles y KPI de informes de Reporting Services más informes de Power BI Desktop. También puede guardar los libros de Excel en el portal.

Siga leyendo para obtener más información sobre estos productos.

> [!NOTE]
> ¿Busca el servidor de informes de BI de energía? Vea [empezar a trabajar con el servidor de informes de Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

### <a name="whats-new-in-reporting-services"></a>Novedades de Reporting Services

Estos orígenes le mantendrán al día sobre las nuevas funciones en SQL Server 2016 Reporting Services.

* [Novedades de Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
* [Blog del equipo de SQL Server Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/)
* Canal de YouTube The [Guy in a Cube](https://www.youtube.com/channel/UCFp1vaKzpfvoGai0vE5VJ0w)

## <a name="paginated-reports"></a>Informes paginados

![ssrs-paginated-reports](../reporting-services/media/ssrs-paginated-reports.png)

Reporting Services está asociado con informes paginados "tradicionales" con un estilo de documento en los que, cuantos más datos tenga, más filas contendrán las tablas y más páginas contendrá el informe. Es un aspecto positivo si queremos generar documentos que tengan un diseño fijo, píxeles perfectos y que estén optimizados para la impresión, como los archivos PDF y los archivos de Word.

Esta carga de trabajo esencial de BI sigue existiendo en la actualidad, por lo que la hemos modernizado. Ahora puede crear informes de aspecto moderno con nuevas características actualizadas, usando [Report Builder](../reporting-services/report-builder/report-builder-in-sql-server-2016.md) o el Diseñador de informes en [SQL Server Data Tools (SSDT)](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).

* Hemos actualizado todos los estilos y paletas de colores predeterminados, de manera que puede crear informes con un nuevo estilo moderno y minimalista de forma predeterminada.
* Hemos actualizado el panel de parámetros para que pueda organizar los parámetros como quiera.
* Puede exportar a nuevos formatos, como PowerPoint. Las visualizaciones de Reporting Services en PowerPoint son activas y se pueden editar; es decir, no son capturas de pantalla.
* Puede crear una experiencia híbrida de Power BI o de Reporting Services: en lugar de volver a crear los informes locales de Reporting Services en Power BI, puede anclar elementos visuales de estos informes en los paneles de Power BI. Luego puede supervisarlo todo desde un lugar en el panel de Power BI.

## <a name="mobile-reports"></a>Informes móviles

![ssrs-mobile-reports](../reporting-services/media/ssrs-mobile-reports.png)

La informática móvil ha cambiado los dispositivos con los que tenemos que trabajar, por lo que, hoy en día, las personas tienen unas necesidades diferentes a la hora de crear informes. La experiencia de los informes de diseño fijo no funciona bien cuando se introducen tabletas y teléfonos. Algo diseñado para una pantalla ancha de PC no es una experiencia óptima en una pequeña pantalla de teléfono, no porque sea más pequeña, sino porque puede tener una orientación vertical u horizontal.

Lo que necesita con estos factores de forma de pantalla claramente diferentes no es un diseño fijo, sino un diseño con capacidad de respuesta que se adapte a los distintos dispositivos y a las distintas formas en que los sostiene. Por este motivo, hemos agregado un nuevo tipo de informe: los informes móviles, que se basan en la tecnología Datazen, que adquirimos hace más o menos un año e integramos en el producto. Puede migrar los informes existentes de Datazen a Reporting Services con el [Asistente para migración de SQL Server para Datazen](https://www.microsoft.com/download/details.aspx?id=53128). 

Puede crear estos informes móviles en la nueva aplicación [Publicador de informes móviles](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) . En las [aplicaciones nativas de Power BI para dispositivos móviles](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) para Windows 10, iOS, Android y HTML5, puede obtener acceso a los datos que tiene en la nube de Power BI, además de los datos locales de SQL Server 2016 Reporting Services. A medida que crea visualizaciones, el Publicador de informes móviles genera automáticamente datos de ejemplo para cada una de ellas; así, puede ver el aspecto que tendrá la visualización con los datos y comprobar qué tipo de datos va bien en cada visualización.

## <a name="web-portal"></a>Portal web

![ssrs-web-portal](../reporting-services/media/ssrs-web-portal.png)

Para los usuarios finales de Reporting Services en modo nativo, la entrada principal es un portal web moderno que se puede ver en cualquier explorador moderno. Puede tener acceso a todos los informes paginados o móviles de Reporting Services y los KPI en el nuevo portal, además de informes de Power BI Desktop. Obtenga más información sobre [informes de Power BI en Reporting Services](../reporting-services/power-bi-reports-in-reporting-services.md).  

Puede aplicar su propia marca personalizada al portal web y puede crear KPI directamente en él. Los KPI pueden hacer que en el explorador aparezcan métricas empresariales clave para que pueda echarles un vistazo sin tener que abrir ningún informe. 

El nuevo portal web es una versión totalmente nueva del Administrador de informes. Ahora se trata de una aplicación HTML5 de una sola página y basada en estándares, para la que los exploradores modernos están optimizados: Edge, Internet Explorer 10 y 11, Chrome, Firefox, Safari y todos los exploradores principales.

El contenido en el portal web se organiza por tipo: informes paginados o móviles de Reporting Services y KPI, además de Power BI Desktop informes, Excel los libros, conjuntos de datos compartidos y orígenes de datos compartidos que se usará como bloques de creación para los informes. Puede almacenar y gestionarlos con seguridad a continuación, en la jerarquía de carpetas tradicional. Puede etiquetar sus favoritos y administrar el contenido si dispone de ese rol.

También puede seguir programando el procesamiento de informes, obtener acceso a los informes a petición y suscribirse a informes publicados en el nuevo portal web.

Obtenga más información sobre la [portal Web (modo nativo de SSRS)](../reporting-services/web-portal-ssrs-native-mode.md).

## <a name="reporting-services-in-sharepoint-integrated-mode"></a>Reporting Services en el modo integrado de SharePoint

Puede publicar informes en Reporting Services en el modo integrado de SharePoint. Puede programar el procesamiento de informes, el acceso a informes a petición, la suscripción a informes publicados y la exportación de informes a otras aplicaciones, como Microsoft Excel. Puede crear también alertas de datos en los informes publicados en un sitio de SharePoint y recibir mensajes de correo electrónico cuando cambien los datos del informe.  

Más información sobre el [Servidor de informes de Reporting Services en el modo integrado de SharePoint](../reporting-services/report-server-sharepoint/reporting-services-report-server-sharepoint-mode.md).

## <a name="includessrsnoversionincludesssrsnoversion-mdmd-programming-features"></a>Características de programación de[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 

Benefíciese de las características de programación de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , para que pueda extender y personalizar la funcionalidad de creación de informes, con API para integrar o extender el procesamiento de datos e informes en aplicaciones personalizadas.

Más [documentación para desarrolladores de Reporting Services](../reporting-services/reporting-services-developer-documentation.md). 

## <a name="next-steps"></a>Pasos siguientes

* [Instalar Reporting Services](../reporting-services/install-windows/install-reporting-services.md)  
* [Instalar el Generador de informes](../reporting-services/install-windows/install-report-builder.md)   
* [Descargar SQL Server Data Tools (SSDT)](http://go.microsoft.com/fwlink/?LinkID=616714)  
* [Informes de Power BI en Reporting Services](../reporting-services/power-bi-reports-in-reporting-services.md)

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)

