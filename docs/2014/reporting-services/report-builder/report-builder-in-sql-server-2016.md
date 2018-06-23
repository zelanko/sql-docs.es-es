---
title: En SQL Server 2014 del generador de informes | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
caps.latest.revision: 29
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ab3d87e730ee8788f010f776899d3d494887ed96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112409"
---
# <a name="report-builder-in-sql-server-2014"></a>Generador de informes en SQL Server 2014
  El Generador de informes es un entorno de creación de informes destinado a los usuarios empresariales que prefieren trabajar en el entorno de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office. Al diseñar un informe, especifica dónde obtener los datos, qué datos obtener y cómo mostrar los datos. Al ejecutar el informe, el procesador de informes toma toda la información especificada, recupera los datos y los combina con el diseño del informe para generar el informe. Puede obtener una vista previa de los informes en el Generador de informes o publicar el informe en un servidor de informes o en un servidor de informes en el modo integrado de SharePoint, donde otros usuarios podrán ejecutarlo.  
  
 El informe de esta ilustración presenta una matriz con grupos de filas y columnas, minigráficos, indicadores y un gráfico circular de resumen en la celda de la esquina, acompañada de un mapa con dos conjuntos de datos geográficos presentados por color y tamaño del círculo.  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="JumpStartReptCreation"></a> Iniciar la creación del informe  
  
-   **Iniciar elementos de informe withreport** creado por otra persona de su equipo. Las partes de informe son elementos de informe que se han publicado aparte en un servidor de informes o en un sitio de SharePoint integrado con un servidor de informes. Se pueden volver a usar en otros informes. Los elementos de informe, como las tablas, las matrices, los gráficos y las imágenes, se pueden publicar como elementos de informe.  
  
-   **Comience con un conjunto de datos compartido** creado por otra persona de su equipo. Los conjuntos de datos compartidos son consultas basadas en un origen de datos compartido almacenadas en un servidor de informes o en un sitio de SharePoint integrado con un servidor de informes.  
  
-   **Comience con la tabla, la matriz o el Asistente para gráficos**. Elija una conexión de origen de datos, arrastre y coloque campos para crear una consulta de conjunto de datos, seleccione un diseño y un estilo y personalice el informe.  
  
-   **Comience con el Asistente para mapas** para crear informes que muestren datos agregados con un fondo geográfico o geométrico. Los datos de mapa pueden ser datos espaciales de una consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] o un archivo de forma del Environmental Systems Research Institute, Inc. (ESRI). También puede agregar un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] fondo de mosaicos de Bing Maps.  
  

  
##  <a name="DesignRept"></a> Diseñar el informe  
  
-   **Crear informes con la tabla, matriz, gráfico y diseños de informe de forma libre.** Cree informes de tabla para datos basados en columnas, informes de matrices (como informes para referencias cruzadas de tabla o para PivotTable) para datos resumidos, informes de gráficos para datos gráficos e informes de formato libre para todo los demás. Los informes pueden incrustar otros informes y gráficos, junto con listas, gráficos y controles para las aplicaciones dinámicas basadas en web.  
  
-   **Informes a partir de diferentes orígenes de datos.** Cree informes con datos de cualquier tipo de origen de datos que tenga un proveedor de datos administrado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], un proveedor OLE DB o un origen de datos ODBC. Puede crear informes que utilizan datos relacionales y multidimensionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion y otras bases de datos. Puede utilizar una extensión de procesamiento de datos XML para recuperar datos desde cualquier origen de datos XML. Puede utilizar funciones con valores de tabla para diseñar orígenes de datos personalizados.  
  
-   **Modifique los informes existentes.** Mediante el generador de informes, puede personalizar y actualizar informes creados en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]el Diseñador de informes.  
  
-   **Modificar los datos** filtrar, agrupar y ordenar datos, o agregando fórmulas o expresiones.  
  
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
  

  
##  <a name="InThisSection"></a> En esta sección  
 [Novedades en el generador de informes para SQL Server 2014](../what-s-new-in-report-builder-for-sql-server-2014.md)  
 Describe las nuevas características de esta versión del Generador de informes, incluidos los mapas.  
  
 [Tutorial: Crear un informe de gráfico rápido sin conexión](tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 Presenta el Generador de informes y los asistentes disponibles para ayudarle a crear los informes. El tutorial proporciona un conjunto de datos para que los use de modo que no tenga que conectarse a un origen de datos para empezar.  
  
 [Planear un informe &#40;generador de informes&#41;](../report-design/planning-a-report-report-builder.md)  
 Proporciona información acerca de lo que debería tener en cuenta antes de empezar a generar el informe.  
  
 [Conceptos de creación de informes &#40;el generador de informes SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 Define conceptos clave usados a lo largo de toda la documentación del Generador de informes.  
  
 [Vista Diseño del informe &#40;generador de informes&#41;](report-design-view-report-builder.md)  
 Explica los diferentes paneles y regiones de la vista de diseño del informe.  
  
 [Vista de diseño de conjunto de datos compartidos &#40;generador de informes&#41;](shared-dataset-design-view-report-builder.md)  
 Explica los diferentes paneles y regiones de la vista de diseño del conjunto de datos compartido.  
  
 [Métodos abreviados de teclado &#40;generador de informes&#41;](keyboard-shortcuts-report-builder.md)  
 Describe las teclas de método abreviado disponibles para navegar y diseñar informes en el Generador de informes.  
  
 [Iniciar el generador de informes &#40;generador de informes&#41;](start-report-builder.md)  
 Explica cómo iniciar las dos versiones distintas del Generador de informes: independiente y [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)].  
  
  