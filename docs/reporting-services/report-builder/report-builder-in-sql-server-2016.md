---
title: En SQL Server 2016 del generador de informes | Documentos de Microsoft
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
caps.latest.revision: 35
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: c2a8702fcee392936451e4a55a4b97327de2b97d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="report-builder-in-sql-server-2016"></a>Generador de informes en SQL Server 2016
  [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] es una herramienta de creación de informes paginados para usuarios profesionales que prefieren trabajar en un entorno independiente en lugar de usar el Diseñador de informes de Visual Studio.  Al diseñar un informe paginado, crea una definición de informe que especifica dónde obtener los datos, qué datos obtener y cómo visualizarlos. Al ejecutar el informe, el procesador de informes usa la definición de informe especificada, recupera los datos y los combina con el diseño del informe para generar el informe. Puede obtener una vista previa del informe en el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] o publicarlo en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo o en modo integrado de SharePoint, donde otros usuarios podrán ejecutarlo.  
  
 ![rs_GettingStartedReport](../../reporting-services/report-builder/media/rs-gettingstartedreport.png "rs_GettingStartedReport")  
  
 En este informe paginado se muestra una matriz con grupos de filas y columnas, minigráficos, indicadores y un gráfico circular de resumen en la celda de la esquina, acompañada de un mapa con dos conjuntos de datos geográficos representados por color y tamaño del círculo.  
  
##  <a name="JumpStartReptCreation"></a> Iniciar la creación del informe  
  
-   **Comience con un conjunto de datos compartido**. Los conjuntos de datos compartidos son consultas basadas en un origen de datos compartido almacenadas en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo o en modo integrado de SharePoint.  
  
-   **Comience con la tabla, la matriz o el Asistente para gráficos**. Elija una conexión de origen de datos, arrastre y coloque campos para crear una consulta de conjunto de datos, seleccione un diseño y un estilo y personalice el informe.  
  
-   **Comience con el Asistente para mapas** para crear informes que muestren datos agregados con un fondo geográfico o geométrico. Los datos de mapa pueden ser datos espaciales de una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] o un archivo de forma del Environmental Systems Research Institute, Inc. (ESRI). También puede agregar un fondo de mosaico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing Maps.  
  
-   **Inicie el informe con elementos de informe**. Los elementos de informe son elementos publicados aparte en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo nativo o en modo integrado de SharePoint. Estos elementos se pueden volver a usar en otros informes. Los elementos de informe, como las tablas, las matrices, los gráficos y las imágenes, se pueden publicar como elementos de informe.  
  
##  <a name="DesignRept"></a> Diseñar el informe  
  
-   **Cree informes paginados con diseños de tabla, matriz, gráfico y formato libre.** Cree informes de tabla para datos basados en columnas, informes de matrices (como informes para referencias cruzadas de tabla o para PivotTable) para datos resumidos, informes de gráficos para datos gráficos e informes de formato libre para todo los demás. Los informes pueden incrustar otros informes y gráficos, junto con listas, gráficos y controles para las aplicaciones dinámicas basadas en web.  
  
-   **Informes a partir de diferentes orígenes de datos.** Cree informes con datos de cualquier tipo de origen de datos que tenga un proveedor de datos administrado por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], un proveedor OLE DB o un origen de datos ODBC. Puede crear informes que utilizan datos relacionales y multidimensionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion y otras bases de datos. Puede utilizar una extensión de procesamiento de datos XML para recuperar datos desde cualquier origen de datos XML. Puede utilizar funciones con valores de tabla para diseñar orígenes de datos personalizados.  
  
-   **Modifique los informes existentes.** Con el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)], puede personalizar y actualizar informes creados en el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   **Modifique los datos** filtrando, agrupando y ordenando los datos o agregando fórmulas o expresiones.  
  
-   **Agregue gráficos, medidores, minigráficos e indicadores** para resumir los datos en un formato visual y presentar grandes volúmenes de información agregada de un vistazo.  
  
-   **Agregue características interactivas** como mapas del documento, botones para mostrar u ocultar, y vínculos de obtención de detalles a subinformes e informes detallados. Utilice parámetros y filtros para filtrar los datos de las vistas personalizadas.  
  
-   **Incruste o haga referencia a imágenes** y a otros recursos, incluidos los contenidos externos.  
  
##  <a name="ManageRpt"></a> Administrar el informe  
  
-   **Guarde la definición del informe** en el equipo o en el servidor de informes, donde podrá administrarlo y compartirlo con otros usuarios.  
  
-   **Elija un formato de presentación** al abrir el informe o después de abrirlo. Puede elegir entre formatos orientados a web o a página, o formatos de aplicaciones de escritorio. Entre estos formatos se incluyen los siguientes: HTML, MHTML, PDF, XML, CSV, TIFF, Word y Excel.  
  
-   **Configure suscripciones.** Una vez publicado el informe en el servidor de informes o en un servidor de informes en el modo integrado de SharePoint, puede configurar el informe para que se ejecute en un momento determinado, crear un historial de informes y configurar suscripciones de correo electrónico.  
  
-   **Genere fuentes de distribución de datos** a partir del informe utilizando la extensión de presentación Atom de Reporting Services.  
  
> [!NOTE]  
>  El administrador del servidor de informes se encarga de administrar los informes publicados en un servidor de informes o un servidor de informes en el modo integrado de SharePoint. Los administradores del servidor de informes pueden definir la seguridad, establecer las propiedades y programar operaciones como el historial de informes y la entrega de informes por correo electrónico. Pueden crear programaciones compartidas y orígenes de datos compartidos, y ponerlos a disposición de todos los usuarios. Los administradores también controlan todas las carpetas del servidor de informes. La posibilidad de realizar tareas de administración depende de los permisos de usuario.  
  
## <a name="see-also"></a>Vea también  
  [Iniciar el Generador de informes](../../reporting-services/report-builder/start-report-builder.md)  
  
  [Instalar el Generador de informes](../../reporting-services/install-windows/install-report-builder.md)

  [Novedades en Reporting Services y el Generador de informes de SQL Server 2016](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)  
  Se describen las nuevas características de esta versión de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].   
  [Tutorial: Crear un informe de gráfico rápido sin conexión](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 Presenta el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] y los asistentes disponibles para ayudarlo a crear los informes. El tutorial proporciona un conjunto de datos para que los use de modo que no tenga que conectarse a un origen de datos para empezar.  
  
 [Planear un informe &#40;Generador de informes&#41;](../../reporting-services/report-design/planning-a-report-report-builder.md)  
 Proporciona información acerca de lo que debería tener en cuenta antes de empezar a generar el informe.  
  
 [Conceptos de creación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 Define conceptos básicos usados en toda la documentación del [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)] .  
  
 [Vista de diseño de informe &#40;Generador de informes&#41;](../../reporting-services/report-builder/report-design-view-report-builder.md)  
 Explica los diferentes paneles y regiones de la vista de diseño del informe.  
  
 [Vista de diseño de conjunto de datos compartidos &#40;Generador de informes&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)  
 Explica los diferentes paneles y regiones de la vista de diseño del conjunto de datos compartido.  
  
 [Métodos abreviados de teclado &#40;Generador de informes&#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
 Se describen las teclas de método abreviado disponibles para navegar y diseñar informes en el [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)].  
  


