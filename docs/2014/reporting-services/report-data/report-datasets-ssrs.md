---
title: Agregar datos a un informe (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2e42303-e355-4c1f-bb3b-3338fbdd230d
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: aeae106d4ab76cb6ab04248126b4b32e1e4a160a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196175"
---
# <a name="add-data-to-a-report-report-builder-and-ssrs"></a>Agregar datos a un informe (Generador de informes y SSRS)
  Para agregar datos a un informe, cree conjuntos de datos. Cada conjunto de datos representa el conjunto de resultados obtenidos al ejecutar un comando de consulta en un origen de datos. Las columnas del conjunto de resultados son la colección de campos y las filas, los datos. Un conjunto de resultados no contiene los datos reales, sino la información necesaria para recuperar un conjunto de datos específico a partir de un origen de datos.  
  
 Hay dos tipos de conjuntos de datos: insertados y compartidos. Los primeros se definen en un informe y se usan solo en ese informe, mientras que los segundos se definen en el servidor de informes o en un sitio de SharePoint y los pueden usar varios informes. En el Generador de informes, puede crear conjuntos de datos compartidos en el modo de conjunto de datos compartido o conjuntos de datos insertados en el modo del Diseñador de informes. En el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], puede crear conjuntos de datos compartidos como parte de un proyecto o conjuntos de datos insertados como parte de un informe.  
  
-   **Conjuntos de datos insertados.** A diferencia de aplicaciones como [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel en las que trabaja con los datos directamente en una hoja de cálculo, en el Generador de informes o el Diseñador de informes trabaja con los metadatos que representen los datos que se recuperarán cuando se procese el informe. Para crear un conjunto de datos insertado, seleccione el origen de datos y especifique una consulta. Después de crear el conjunto de datos, use el panel Datos de informe para ver la colección de campos. Puede mostrar datos desde un conjunto de datos en una región de datos como una tabla o un gráfico. En cada región de datos, puede agrupar, filtrar y ordenar los datos para organizarlos. Una vez que haya terminado el diseño del informe, ejecútelo para ver los datos reales.  
  
     En la siguiente figura, el panel Datos de informe muestra un origen de datos denominado [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)], un conjunto de datos denominado DataSet1 y cinco campos en la colección de campos del conjunto de datos. En el panel Diseño se muestra una tabla con la fila superior de encabezados de columna y la fila inferior con celdas de tabla que contienen texto. El texto del marcador de posición [Name] son los metadatos para el campo Name. Cuando se ejecuta el informe, los valores de los datos reales reemplazan el texto del marcador de posición. La tabla se expande lo necesario para mostrar todos los datos.  
  
     ![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
-   **Conjuntos de datos compartidos.** Cree un conjunto de datos compartidos cuando desee usar un conjunto de datos en varios informes. Para crear y guardar un conjunto de datos en un servidor de informes o en un sitio de SharePoint, use el Diseñador de informes en la vista de diseño del conjunto de datos compartido. Para crear un conjunto de datos compartido como parte de un proyecto que se pueda implementar en un servidor o en un sitio, use el Diseñador de informes.  
  
     En la ilustración siguiente se muestra la vista de diseño de conjunto de datos compartido del Generador de informes. Puede seleccionar o modificar la conexión de datos, las propiedades del conjunto de datos, la consulta, los filtros y, opcionalmente, puede marcar los filtros como parámetros y ver los resultados de la consulta. A continuación, guarde los cambios en el servidor o en un sitio.  
  
     ![rs_SharedDatasetDesignMode](../media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 Para más información, vea [Conjuntos de datos incrustados y compartidos &#40;Generador de informes y SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md) y [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 Además, puede agregar conjuntos de datos a un informe agregando elementos de informe que incluyan los conjuntos de datos de los que dependen. [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 Para aprender a crear un informe donde se muestren datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../tutorial-creating-a-basic-table-report-report-builder.md). Para crear un informe que contenga sus propios datos, vea [Tutorial: Crear un informe de gráfico rápido sin conexión &#40;Generador de informes&#41;](../report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Methods"></a> Agregar los datos del informe  
 En el Generador de informes, puede agregar los datos del informe de las siguientes formas.  
  
-   Agregar a un informe elementos de informe de un servidor de informes. Cada elemento de informe es autónomo e incluye los conjuntos de datos dependientes. Los conjuntos de datos están predefinidos.  
  
-   Usar los asistentes para tablas, matrices, gráficos y mapas. A partir de los asistentes, puede seleccionar orígenes de datos compartidos y conjuntos de datos compartidos. O bien, crear nuevos conjuntos de datos y continuar con el diseño del informe.  
  
-   Agregar conjuntos de datos compartidos de un servidor de informes. Los conjuntos de datos compartidos están predefinidos y especifican los datos que se deben usar de un origen de datos predefinido. Cuando agregue un conjunto de datos compartido a un informe, lo que agrega es la referencia de un conjunto de datos que señale a la definición del conjunto de datos compartido.  
  
 En el Generador de informes o en el Diseñador de informes, puede agregar los datos del informe de las siguientes formas.  
  
-   Agregar conjuntos de datos insertados basados en orígenes de datos compartidos.  
  
-   Agregar conjuntos de datos insertados basados en orígenes de datos insertados.  
  
> [!NOTE]  
>  En un servidor de informes, los elementos compartidos se protegen individualmente o heredando los permisos de la carpeta donde se publican. Para permitir que otros usuarios tengan acceso a los conjuntos de datos compartidos que guarde, debe saber cómo se conceden los permisos. Para más información, vea [Seguridad &#40;Generador de informes&#41;](../report-builder/security-report-builder.md) o [Proteger los elementos de un conjunto de datos compartido](../security/secure-shared-dataset-items.md).  
  
 Después de agregar datos a un informe, puede organizar los datos en la página del informe con regiones de datos, modificar los elementos de informe y compartir los cambios con otros usuarios. Además, puede permitir que los usuarios ordenen o limiten los datos que se ven en el informe. Para obtener más información, vea los siguientes temas relacionados:  
  
-   [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
-   [Gráficos &#40;el generador de informes SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
-   [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
-   [Indicadores &#40;Generador de informes y SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)  
  
-   [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Elementos de informe &#40;el generador de informes SSRS&#41;](../report-parts-report-builder-and-ssrs.md)  
  
-   [Filtrar, agrupar y ordenar datos &#40;el generador de informes SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="QuickStart"></a> Agregar datos con los elementos de informe  
 Los elementos de informe contienen los conjuntos de datos de los que dependen. Estos conjuntos de datos se generan en orígenes de datos compartidos disponibles en el servidor de informes. En el Generador de informes, cuando agregue un elemento de informe a un informe, también se agregan los conjuntos de datos dependientes, como si los hubiera agregado manualmente. Por ejemplo, un gráfico predefinido contiene un conjunto de datos. Para ver los datos, obtenga una vista previa del informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 Los elementos de informe, los orígenes de datos compartidos y los conjuntos de datos compartidos se definen de antemano y se guardan en un servidor de informes. Para tener acceso a ellos, debe abrir el Generador de informes en modo de servidor mediante una conexión al servidor de informes. Puede usarlos para crear nuevas versiones si tiene permisos de escritura en el servidor de informes.  
  
-   Para más información, vea [Elementos de informe &#40;Generador de informes y SSRS&#41;](../report-parts-report-builder-and-ssrs.md) y [Elementos de informe en el Diseñador de informes &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Queries"></a> Consultas y diseñadores de consultas  
 Para especificar los datos que desee de un origen de datos, compile un comando de consulta. Cada tipo de origen de datos proporciona un *diseñador de consultas* relacionado para ayudarle a compilar la consulta. El diseñador de consultas puede ser gráfico o estar basado en texto. En un diseñador gráfico de consultas, puede ver los metadatos que representan los datos del origen de datos externo y crear interactivamente una consulta arrastrando campos o entidades hasta la superficie de diseño de la consulta. En un diseñador de consultas basado en texto, debe escribir, o importar, consultas en la sintaxis de consulta admitida por el origen de datos externo.  
  
 En el diseñador de consultas, puede ejecutar la consulta para ver datos de ejemplo y validar la sintaxis del comando de consulta. Los nombres de columna del conjunto de resultados se convierten en los nombres de campo que se ven en el panel Datos de informe. El conjunto de resultados debe ser un conjunto único de filas y columnas en el que existe el mismo número de valores para cada fila de datos. No se admiten varios conjuntos de resultados de una única consulta. Las jerarquías desiguales, que no tienen un número constante de columnas y pueden generar un número distinto de valores de datos para cada fila, no se admiten.  
  
 Para ejecutar una consulta, debe tener credenciales de tiempo de diseño. Para obtener más información, consulte [especificar credenciales en el generador de informes](../specify-credentials-in-report-builder.md) y [las conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 Los proveedores de datos se ocupan de la comunicación entre una extensión de datos y el origen de datos externo. Cada proveedor de datos determina la compatibilidad con la sintaxis de comandos de consulta, los parámetros de consulta y los tipos de datos de los valores en el conjunto de resultados. Para más información, vea el tema del tipo específico de extensión de datos y [Diseñadores de consultas &#40;Generador de informes&#41;](../query-designers-report-builder.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;el generador de informes SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar, editar y actualizar campos en el panel Datos de informe &#40;Generador de informes y SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
 [Crear una consulta en el Diseñador de consultas relacionales &#40;el generador de informes SSRS&#41;](build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)  
  
 [Mostrar conjuntos de datos ocultos para los valores de parámetro de datos multidimensionales &#40;el generador de informes SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 [Establecer un mensaje no hay datos para una región de datos &#40;el generador de informes SSRS&#41;](set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Asociar un parámetro de consulta con un parámetro de informe &#40;el generador de informes SSRS&#41;](associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)  
  
 [Definir los parámetros en el Diseñador de consultas MDX para Analysis Services &#40;el generador de informes SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Section"></a> En esta sección  
 [Elementos de informe y conjuntos de datos en el Generador de informes](report-parts-and-datasets-in-report-builder.md)  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
 [Especifique credenciales en el generador de informes](../specify-credentials-in-report-builder.md)  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
## <a name="see-also"></a>Vea también  
 [Vista de diseño de informe &#40;Generador de informes&#41;](../report-builder/report-design-view-report-builder.md)   
 [Conceptos de creación de informes &#40;el generador de informes SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
  
  