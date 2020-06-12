---
title: Tutorial del diagrama del clúster (complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: 578b5b8e55fd3ae660db985eed2e608667dc768b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527491"
---
# <a name="cluster-diagram-walkthrough-data-mining-add-ins"></a>Tutorial del diagrama del clúster (Complementos de minería de datos)
  Después de crear un modelo de agrupación en clústeres, puede importarlo en Visio con la forma **agrupar** y, a continuación, seguir personalizando y mejorando el diseño. Las **formas de minería de datos para Visio** incluyen los siguientes controles personalizados para trabajar con diagramas de minería de datos:  
  
-   Representar los controles del diagrama de clúster  
  
     Estas opciones forman parte del **Asistente para clúster** que se inicia cuando se coloca una forma en el área de trabajo de Visio.  
  
-   Barra de herramientas de **diseño de minería de datos**  
  
     Estas opciones se agregan al área de trabajo de Visio con el fin de ayudarle a interactuar con la forma de minería de datos. Las opciones son diferentes en función del tipo de datos del modelo de minería de datos que esté usando.  
  
## <a name="build-a-cluster-diagram"></a>Generar un diagrama de clúster  
 Este tutorial muestra cómo crear y personalizar un diagrama de agrupación de clúster en Visio.  
  
 Para poder continuar, deberá tener ya disponible un modelo de agrupación en clústeres. Si no tiene un modelo, use el asistente [para clúster &#40;complementos de minería de datos para el Asistente para&#41;de Excel](cluster-wizard-data-mining-add-ins-for-excel.md) y cree un modelo mediante el conjunto de datos de entrenamiento del libro de ejemplo, con todos los valores predeterminados.  
  
#### <a name="use-the-cluster-visio-shape-wizard"></a>Usar el Asistente para crear formas clúster de Visio  
  
1.  Si no ve formas de **minería de datos de Microsoft** en la lista **formas** , haga clic en **más formas**, seleccione **Abrir Galería de símbolos**y abra la plantilla desde la ubicación de instalación predeterminada.  
  
     \<drive>: \Archivos de Programa\microsoft SQL Server 2012 DM-ins  
  
2.  Arrastre la forma **clúster** hasta la página.  
  
3.  En la página de bienvenida del **Asistente para crear formas clúster de Visio**, haga clic en **siguiente**.  
  
4.  En la página **seleccionar un origen de datos** del **Asistente para clúster**, elija una conexión a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que contenga los modelos de minería de datos que desea visualizar.  
  
5.  Seleccione un modelo de minería de datos adecuado y haga clic en **siguiente**.  
  
     Para asegurarse de que elige un modelo de agrupación en clústeres, revise la descripción en el panel **propiedades** .  
  
6.  Si la conexión se realiza correctamente, en la página **Opciones del diagrama del clúster**, decida qué tipo de diagrama de clúster desea incluir en la presentación de Visio:  
  
     **Mostrar sólo formas de clúster**  
     Esta opción crea un diagrama del clúster sencillo, donde cada clúster queda representado por un rectángulo u otra forma que elija  
  
     **Mostrar clústeres con gráfico de características**  
     Esta opción crea el mismo gráfico que anteriormente, pero dentro de las formas habrá histogramas que describen las características del clúster.  
  
     ![Ejemplo de gráfico de características de clúster en Visio](media/dm13-visio-cluster-samplecharshape.gif "Ejemplo de gráfico de características de clúster en Visio")  
  
     **Mostrar clústeres con gráfico de distinción**  
     Esta opción crea el mismo gráfico que el diagrama del clúster, pero enumera las características del clúster actual que lo diferencian con mayor claridad de otros clústeres.  
  
     Puede cambiar a otro tipo de gráfico después de que el asistente haya generado el diagrama; para ello, haga clic con el botón secundario y seleccione un tipo de gráfico nuevo. Por ahora, elija la opción **Mostrar clústeres con el gráfico de características**.  
  
7.  Deje la opción **número de filas en el gráfico**, como 5.  
  
     Esta opción no cambia el número de clústeres del modelo; simplemente limita el número de atributos que se pueden mostrar como características de cada clúster.  
  
     Sin embargo, la opción actúa como filtro en los datos del gráfico, por lo que no puede aumentar el número de elementos más adelante.  
  
8.  Haga clic en **Avanzado**.  
  
     El cuadro de diálogo **Opciones de clúster** es donde se personaliza la apariencia visual de las formas utilizadas en el diagrama. Puede cambiar los colores que se usan en el gráfico, así como las formas de los clústeres.  
  
     El control de **variable de sombreado** no funciona en Office 2013.  
  
     ![hacer clic en Avanzadas para seleccionar colores de forma](media/dm13-visio-clusteroptions-advanced.gif "hacer clic en Avanzadas para seleccionar colores de forma")  
  
     **Sugerencia:** Algunos colores se pueden modificar posteriormente mediante los temas de Visio y los controles de edición de formas. Sin embargo, los temas de Visio también invalidarán algunas de estas selecciones de color, por lo que se recomienda comenzar con los colores predeterminados e ir aplicando cambios paulatinamente.  
  
9. Haga clic en **Finalizar** para crear el gráfico.  
  
     El asistente recupera información del modelo de minería de datos, crea las formas y rellena cada clúster con atributos y valores.  
  
     ![una red de dependencias](media/dm13-visiodepnet-defaultgraph.gif "una red de dependencias")  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar y modificar el diagrama finalizado  
 Una vez haya completado el diagrama, puede seguir personalizando la apariencia mediante los controles de Visio, tal como se muestra en el siguiente ejemplo.  
  
 ![Diagrama de clúster personalizado con Visio](media/dm13-visio-clustercomplete1.gif "Diagrama de clúster personalizado con Visio")  
  
 El asistente genera todas las formas básicas de clústeres; use las herramientas siguientes para actualizar y personalizar el diagrama:  
  
1.  Arrastre el control deslizante del control **Opciones de clúster** para filtrar las relaciones más débiles y simplificar el diagrama.  
  
2.  Use la opción **de página rediseño** de Visio para experimentar con distintos diseños de clúster.  
  
3.  Use la opción **conectores** en la pestaña **diseño** para cambiar el estilo del conector y evitar que las líneas crucen los clústeres.  
  
4.  Haga clic en la cinta de opciones de **Complementos** y, a continuación, muestre una de las barras de herramientas personalizadas que se usan para trabajar con diagramas de minería de datos:  
  
     **Diseño**  
     Optimiza la organización de los clústeres para que se ajusten en la página actual.  
  
     **Cambiar tamaño de página**  
     Este control se ha diseñado para la versiones anteriores de HTML. En su lugar, use la página de Visio para cambiar el tamaño de los controles.  
  
     **Descripción**  
     Si selecciona un clúster, haga clic en esta opción para mostrar los detalles sobre el clúster.  
  
     ![hacer clic en Descripción para obtener detalles acerca del clúster](media/dm13-visio-cluster-description-control.gif "hacer clic en Descripción para obtener detalles acerca del clúster")  
  
     **Intensidad del borde**  
     Muestra las puntuaciones de confianza en las líneas que conectan los clústeres.  
  
     Sin embargo, si aplica algún formato especial distinto del predeterminado que genera el asistente, lo cual incluye algunos fondos, es posible que estos números no estén visibles.  
  
     **Slider**  
     Filtra las líneas entre los clústeres. Si se sube el control deslizante, se quitan todas las asociaciones salvo las más importantes.  
  
     **Sombreado**  
     Este control no funciona en Office 2013.  
  
5.  Use el control **panorámica y zoom** , en el área del **Panel de tareas** de la cinta de opciones **vista** de Visio, para centrarse en un conjunto de clústeres y desplazarse por el diagrama.  
  
6.  Haga clic con el botón secundario en cualquier clúster para ver las opciones específicas de la forma del clúster:  
  
    -   Cambie el tipo de gráfico.  
  
    -   Agregue un gráfico de características de clúster.  
  
    -   Agregue un gráfico de distinción.  
  
## <a name="see-also"></a>Consulte también  
 [Solucionar problemas de diagramas de minería de datos de Visio &#40;SQL Server complementos de minería de datos&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
