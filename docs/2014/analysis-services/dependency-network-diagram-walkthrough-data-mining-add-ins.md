---
title: Tutorial del diagrama de red de dependencias (complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Visio shapes, dependency network
- shapes, data mining
- shapes, network
- dependencies
- diagram, dependency network
- data mining layout toolbar
- dependency network
ms.assetid: aac732a8-5262-4649-b7d7-3ccf6f9cfa8b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: db069b243a0d06c142651ab4dcadd68e1e06657f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081969"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>Tutorial del diagrama de red de dependencias (Complementos de minería de datos)
  Existen diversos tipos de modelos de minería de datos que usan gráficos de red como una forma para explorar las relaciones entre los datos. Puede importar estos modelos en Visio con la forma **red de dependencias** y, a continuación, seguir personalizando y mejorando el diseño. Las **formas de minería de datos para Visio** incluyen los siguientes controles personalizados para trabajar con diagramas de red de dependencias:  
  
-   Representar controles para el gráfico de red  
  
     Estas opciones forman parte del asistente que se inician cuando se coloca una forma en el área de trabajo de Visio.  
  
-   Barra de herramientas de **diseño de minería de datos**  
  
     Estas opciones se agregan al área de trabajo de Visio con el fin de ayudarle con el gráfico de red de dependencias.  
  
## <a name="build-a-dependency-network-graph"></a>Generar un gráfico de red de dependencias  
 Coloque una forma en la página de Visio para iniciar el **Asistente para crear formas de red de dependencias de .net** y establecer opciones de diagrama.  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>Usar el Asistente para crear formas red de dependencias de Visio  
  
1.  Si no ve formas de **minería de datos de Microsoft** en la lista **formas** , haga clic en **más formas**, seleccione **Abrir Galería de símbolos**y abra la plantilla desde la ubicación de instalación predeterminada.  
  
     \<> de unidad: \Archivos de programa (x85) \Microsoft SQL Server 2012 DM-ins  
  
2.  Arrastre la forma **red de dependencias** hasta la página para iniciar el asistente. Haga clic en **Siguiente**.  
  
3.  En la página de bienvenida del **Asistente para crear formas red de dependencias de Visio**, haga clic en **siguiente**.  
  
4.  En la página **seleccionar un origen de datos** del **Asistente para crear formas red de dependencias de Visio**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] elija una conexión a un servidor que tenga el modelo que desea visualizar.  
  
5.  Seleccione un modelo de minería de datos adecuado y haga clic en **siguiente**.  
  
     Para seleccionar un modelo adecuado, puede revisar el nombre, la descripción, las columnas y el tipo de datos en el panel **propiedades** .  
  
     Esta forma admite modelos que se hayan creado con estos algoritmos:  
  
    -   Bayes Naive  
  
    -   Árboles de decisión  
  
    -   Reglas de asociación  
  
6.  En la página, **Seleccione los nodos que se van a representar**, personalice el tamaño del gráfico y, si lo desea, filtre solo para incluir determinados nodos.  
  
     Con un conjunto de objetos grande, un gráfico de dependencias puede ser enorme y contener muchos objetos relacionados, representados como *nodos*. Mediante este cuadro de diálogo, podrá crear un gráfico de red personalizado que incluya solo los nodos de interés.  
  
     [marcador de posición Art]  
  
     **Número de nodos que va a capturar**  
     Si el modelo contiene menos nodos de los que se ha especificado, este valor no tiene ningún efecto. Si el modelo contiene más nodos de los que se han especificado, solo se mostrarán los nodos más determinantes.  
  
     **El nombre contiene**  
     Deje este cuadro en blanco y haga clic en la flecha verde para recuperar todos los nodos del modelo.  
  
     O bien, escriba una cadena y haga clic en la flecha verde para devolver solo los nodos que contienen la cadena especificada.  
  
     La mayoría de los modelos que puede crear con los datos de ejemplo no son grandes, por lo tanto, para este ejemplo, incremente el número de nodos a 10 y haga clic en la flecha verde para ejecutar una consulta y obtener la lista de todos los nodos.  
  
7.  Haga clic en **avanzadas** para establecer las opciones de sombreado y forma del gráfico.  
  
8.  Haga clic en **cerrar** para salir del cuadro de diálogo Opciones **avanzadas** y, a continuación, haga clic en **Finalizar** para crear el gráfico.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar y modificar el diagrama finalizado  
 Una vez que Visio ha creado el gráfico de red de dependencias, podrá proseguir con la modificación y mejora del gráfico mediante las características de Visio.  
  
 El gráfico siguiente muestra el diseño predeterminado de un gráfico de red de dependencias.  
  
 [marcador de posición Art]  
  
1.  Use el control **panorámica y zoom** , en el área del **Panel de tareas** de la cinta de opciones **vista** de Visio, para centrarse en una sección del gráfico y desplazarse por el diagrama.  
  
2.  Experimente con distintos diseños de gráfico proporcionados por la opción **de página rediseño** de Visio.  
  
3.  Haga clic en la cinta de opciones de **Complementos** y, a continuación, muestre una de las barras de herramientas personalizadas que se usan para trabajar con diagramas de minería de datos:  
  
     **Diseño**  
     Optimiza el diseño de los nodos en la página y cambia la vista de manera que todos los nodos estén visibles.  
  
     **Cambiar tamaño de página**  
     Cambia el tamaño de la página de manera que todos los nodos estén visibles.  
  
     **Intensidad del borde**  
     Alterna la presentación de la intensidad del borde para todo el gráfico. Un borde es una conexión entre nodos. Puede utilizar el control deslizante para filtrar las conexiones que no son fuertes.  
  
     **Slider**  
     El **control deslizante** le ayuda a controlar la intensidad de las relaciones que se muestran en el diagrama de red de dependencias.  
  
     Cada nodo del gráfico representa un estado. Una flecha representa una transición entre dos estados y la probabilidad asociada a la transición. Para reducir el número de nodos del gráfico, mueva la barra del control deslizante hacia arriba.  
  
     Para aumentar el número de nodos del gráfico, mueva la barra del control deslizante hacia abajo.  
  
     **Agregar elementos**  
     Abre el cuadro de diálogo **seleccionar los nodos que se van a representar** para que pueda seleccionar los nuevos nodos que desea agregar al gráfico.  
  
4.  Puede hacer que los gráficos sean todo lo sencillos o elaborados que desee, así como agregar anotaciones mientras está conectado al modelo.  
  
     [art placeholder]  
  
> [!WARNING]  
>  El resaltado de los nodos dependientes y otras opciones del menú contextual que estaban disponibles en versiones anteriores de los complementos no funcionan en Office 2013.  
  
## <a name="see-also"></a>Consulte también  
 [Solucionar problemas de diagramas de minería de datos de Visio &#40;SQL Server complementos de minería de datos&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
