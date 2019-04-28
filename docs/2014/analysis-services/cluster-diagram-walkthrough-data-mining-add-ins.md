---
title: Tutorial del diagrama (complementos de minería de datos) del clúster | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, cluster
- diagram, cluster
- shapes, data mining
- shapes, cluster
- data mining layout toolbar
ms.assetid: 761bef6a-37d4-4b19-944e-f2aadc75a242
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee4a7a09471078753589463c058ba5ea2e39c4d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680960"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Tutorial del diagrama del clúster (Complementos de minería de datos)
  Después de haber creado un modelo de agrupación en clústeres, puede importarlo en Visio con el **clúster** dar forma y, a continuación, seguir personalizando y mejorando el diseño. El **formas de minería de datos para Visio** incluyen los siguientes controles personalizados para trabajar con diagramas de minería de datos:  
  
-   Representar los controles del diagrama de clúster  
  
     Estas opciones forman parte de la **Asistente para clúster** que se inicia cuando se coloca una forma en el área de trabajo de Visio.  
  
-   **Diseño de minería de datos** barra de herramientas  
  
     Estas opciones se agregan al área de trabajo de Visio con el fin de ayudarle a interactuar con la forma de minería de datos. Las opciones son diferentes en función del tipo de datos del modelo de minería de datos que esté usando.  
  
## <a name="build-a-cluster-diagram"></a>Generar un diagrama de clúster  
 Este tutorial muestra cómo crear y personalizar un diagrama de agrupación de clúster en Visio.  
  
 Para poder continuar, deberá tener ya disponible un modelo de agrupación en clústeres. Si no tiene un modelo, use el [Asistente para clúster &#40;complementos minería de datos para Excel&#41; ](cluster-wizard-data-mining-add-ins-for-excel.md) asistente y crear un modelo usando el conjunto de datos de entrenamiento en el libro de ejemplo, con todos los valores predeterminados.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Utilice al Asistente para formas de Visio de clúster  
  
1.  Si no ve **formas de minería de datos de Microsoft** en el **formas** lista, haga clic en **más formas**, seleccione **Abrir galería de símbolos**y abra el plantilla de la ubicación de instalación predeterminada.  
  
     \<unidad >: \Program files\Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Arrastre el **clúster** forma en la página.  
  
3.  En la página principal de la **Asistente para crear formas de clúster de Visio**, haga clic en **siguiente**.  
  
4.  En el **seleccionar un origen de datos** página de la **Asistente para clúster**, elegir una conexión a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que contiene los modelos de minería de datos que desea visualizar.  
  
5.  Seleccione un modelo de minería de datos adecuado y haga clic en **siguiente**.  
  
     Para asegurarse de elegir un modelo de agrupación en clústeres, revise la descripción en el **propiedades** panel.  
  
6.  Si la conexión es correcta, en la página, **opciones de diagrama del clúster**, decidir qué tipo de diagrama del clúster debe incluir en la presentación de Visio:  
  
     **Mostrar sólo formas de clúster**  
     Esta opción crea un diagrama del clúster sencillo, donde cada clúster queda representado por un rectángulo u otra forma que elija  
  
     **Mostrar clústeres con gráfico de características**  
     Esta opción crea el mismo gráfico que anteriormente, pero dentro de las formas habrá histogramas que describen las características del clúster.  
  
     ![Ejemplo de gráfico de características de clúster en Visio](media/dm13-visio-cluster-samplecharshape.gif "ejemplo de gráfico de características de clúster en Visio")  
  
     **Mostrar clústeres con gráfico de distinción**  
     Esta opción crea el mismo gráfico que el diagrama del clúster, pero enumera las características del clúster actual que lo diferencian con mayor claridad de otros clústeres.  
  
     Puede cambiar a otro tipo de gráfico después de que el asistente haya generado el diagrama; para ello, haga clic con el botón secundario y seleccione un tipo de gráfico nuevo. Por ahora, elija la opción **Mostrar clústeres con gráfico de características**.  
  
7.  Deje la opción **número de filas en el gráfico**, como 5.  
  
     Esta opción no cambia el número de clústeres del modelo; simplemente limita el número de atributos que se pueden mostrar como características de cada clúster.  
  
     Sin embargo, la opción actúa como un filtro en los datos del gráfico, por lo que no puede aumentar el número de elementos más adelante.  
  
8.  Haga clic en **Avanzadas**.  
  
     El **opciones de clúster** cuadro de diálogo es donde personaliza la apariencia visual de las formas utilizadas en el diagrama. Puede cambiar los colores que se usan en el gráfico, así como las formas de los clústeres.  
  
     El **Variable de sombreado** control no funciona en Office 2013.  
  
     ![Haga clic en Avanzadas para seleccionar colores de forma](media/dm13-visio-clusteroptions-advanced.gif "haga clic en Avanzadas para seleccionar los colores de las formas")  
  
     **Sugerencia:** Algunos colores se pueden modificar posteriormente mediante el uso de los temas de Visio y la forma que los controles de edición. Sin embargo, los temas de Visio también invalidarán algunas de estas selecciones de color, por lo que se recomienda comenzar con los colores predeterminados e ir aplicando cambios paulatinamente.  
  
9. Haga clic en **finalizar** para crear el gráfico.  
  
     El asistente recupera información del modelo de minería de datos, crea las formas y rellena cada clúster con atributos y valores.  
  
     ![una red de dependencias](media/dm13-visiodepnet-defaultgraph.gif "una red de dependencias")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar y modificar el diagrama finalizado  
 Una vez haya completado el diagrama, puede seguir personalizando la apariencia mediante los controles de Visio, tal como se muestra en el siguiente ejemplo.  
  
 ![diagrama de clúster personalizado con Visio](media/dm13-visio-clustercomplete1.gif "diagrama de clúster personalizado con Visio")  
  
 El asistente genera todas las formas básicas de clústeres; use las herramientas siguientes para actualizar y personalizar el diagrama:  
  
1.  Arrastre el control deslizante el **opciones de clúster** control, para filtrar las relaciones más débiles y simplificar el diagrama.  
  
2.  Utilice el Visio **rediseñar página** opción para experimentar con diseños de clúster diferente.  
  
3.  Use la **conectores** opción el **diseño** tab para cambiar el estilo de conector para evitar que las líneas pasen por los clústeres.  
  
4.  Haga clic en el **Add-Ins** la cinta de opciones y, a continuación, mostrar una de las barras de herramientas personalizados utilizados para trabajar con diagramas de minería de datos:  
  
     **Diseño**  
     Optimiza la organización de los clústeres para que se ajusten en la página actual.  
  
     **Cambiar el tamaño de página**  
     Este control se ha diseñado para la versiones anteriores de HTML. En su lugar, use la página de Visio para cambiar el tamaño de los controles.  
  
     **Descripción**  
     Si selecciona un clúster, haga clic en esta opción para mostrar los detalles sobre el clúster.  
  
     ![Haga clic para obtener detalles sobre el clúster](media/dm13-visio-cluster-description-control.gif "haga clic para obtener detalles acerca del clúster")  
  
     **Intensidad del borde**  
     Muestra las puntuaciones de confianza en las líneas que conectan los clústeres.  
  
     Sin embargo, si aplica algún formato especial distinto del predeterminado que genera el asistente, lo cual incluye algunos fondos, es posible que estos números no estén visibles.  
  
     **Slider**  
     Filtra las líneas entre los clústeres. Si se sube el control deslizante, se quitan todas las asociaciones salvo las más importantes.  
  
     **Shading**  
     Este control no funciona en Office 2013.  
  
5.  Use la **panorámica y Zoom** controlar, en el **panel de tareas** área de la Visio **vista** cinta de opciones para centrarse en un conjunto de clústeres y desplazarse por el diagrama.  
  
6.  Haga clic con el botón secundario en cualquier clúster para ver las opciones específicas de la forma del clúster:  
  
    -   Cambie el tipo de gráfico.  
  
    -   Agregue un gráfico de características de clúster.  
  
    -   Agregue un gráfico de distinción.  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de diagramas de minería de datos de Visio &#40;complementos de minería de datos de SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
