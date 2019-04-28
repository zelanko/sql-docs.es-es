---
title: Tutorial del diagrama red de dependencias (complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 0f8d69e97aa542d89291d81d60177e520e6a007b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732181"
---
# <a name="dependency-network-diagram-walkthrough-data-mining-add-ins"></a>Tutorial del diagrama de red de dependencias (Complementos de minería de datos)
  Existen diversos tipos de modelos de minería de datos que usan gráficos de red como una forma para explorar las relaciones entre los datos. Puede importar estos modelos en Visio con el **red de dependencias** dar forma y, a continuación, seguir personalizando y mejorando el diseño. El **formas de minería de datos para Visio** incluyen los siguientes controles personalizados para trabajar con diagramas de red de dependencia:  
  
-   Representar controles para el gráfico de red  
  
     Estas opciones forman parte del asistente que se inician cuando se coloca una forma en el área de trabajo de Visio.  
  
-   **Diseño de minería de datos** barra de herramientas  
  
     Estas opciones se agregan al área de trabajo de Visio con el fin de ayudarle con el gráfico de red de dependencias.  
  
## <a name="build-a-dependency-network-graph"></a>Generar un gráfico de red de dependencias  
 Se coloca una forma en la página de Visio para iniciar el **dependencia neto Visio forma asistente** y establecer las opciones del diagrama.  
  
#### <a name="use-the-dependency-net-visio-shape-wizard"></a>Use el Asistente para formas de Visio neto de dependencia  
  
1.  Si no ve **formas de minería de datos de Microsoft** en el **formas** lista, haga clic en **más formas**, seleccione **Abrir galería de símbolos**y abra el plantilla de la ubicación de instalación predeterminada.  
  
     \<unidad >: \Program files (x85) \Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Arrastre el **red de dependencias** forma en la página para iniciar el asistente. Haga clic en **Siguiente**.  
  
3.  En la página principal de la **Asistente para formas de Visio de red de dependencia**, haga clic en **siguiente**.  
  
4.  En el **seleccionar un origen de datos** página de la **Asistente para formas de Visio de red de dependencia**, elegir una conexión a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que contiene el modelo que desea visualizar.  
  
5.  Seleccione un modelo de minería de datos adecuado y haga clic en **siguiente**.  
  
     Para seleccionar un modelo adecuado, puede revisar el nombre, descripción, las columnas y tipo de datos de la **propiedades** panel.  
  
     Esta forma admite modelos que se hayan creado con estos algoritmos:  
  
    -   naive Bayes  
  
    -   Árboles de decisión  
  
    -   Reglas de asociación  
  
6.  En la página, **seleccionar nodos que se representarán**, personalizar el tamaño del gráfico y, opcionalmente, filtrar para incluir solamente algunos nodos.  
  
     Con un conjunto de datos grande, un gráfico de dependencias puede volverse enorme y contener muchos objetos relacionados, representados como *nodos*. Mediante este cuadro de diálogo, podrá crear un gráfico de red personalizado que incluya solo los nodos de interés.  
  
     [marcador de posición de arte]  
  
     **Número de nodos que se va a capturar**  
     Si el modelo contiene menos nodos de los que se ha especificado, este valor no tiene ningún efecto. Si el modelo contiene más nodos de los que se han especificado, solo se mostrarán los nodos más determinantes.  
  
     **El nombre contiene**  
     Deje este cuadro en blanco y haga clic en la flecha verde para recuperar todos los nodos del modelo.  
  
     O bien, escriba una cadena y haga clic en la flecha verde para devolver solo los nodos que contienen la cadena especificada.  
  
     La mayoría de los modelos que puede crear con los datos de ejemplo no son grandes, por lo tanto, para este ejemplo, incremente el número de nodos a 10 y haga clic en la flecha verde para ejecutar una consulta y obtener la lista de todos los nodos.  
  
7.  Haga clic en **avanzadas** para establecer las opciones de sombreado y forma del gráfico.  
  
8.  Haga clic en **cerrar** para salir del **avanzadas** cuadro de diálogo Opciones y, a continuación, haga clic en **finalizar** para crear el gráfico.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar y modificar el diagrama finalizado  
 Una vez que Visio ha creado el gráfico de red de dependencias, podrá proseguir con la modificación y mejora del gráfico mediante las características de Visio.  
  
 El gráfico siguiente muestra el diseño predeterminado de un gráfico de red de dependencias.  
  
 [marcador de posición de arte]  
  
1.  Use la **panorámica y Zoom** controlar, en el **panel de tareas** área de la Visio **vista** cinta de opciones para centrarse en una sección del gráfico y desplazarse por el diagrama.  
  
2.  Experimente con distintos diseños de gráfico proporcionada por el Visio **rediseñar página** opción.  
  
3.  Haga clic en el **Add-Ins** la cinta de opciones y, a continuación, mostrar una de las barras de herramientas personalizados utilizados para trabajar con diagramas de minería de datos:  
  
     **Diseño**  
     Optimiza el diseño de los nodos en la página y cambia la vista de manera que todos los nodos estén visibles.  
  
     **Cambiar el tamaño de página**  
     Cambia el tamaño de la página de manera que todos los nodos estén visibles.  
  
     **Intensidad del borde**  
     Alterna la presentación de la intensidad del borde para todo el gráfico. Un borde es una conexión entre nodos. Puede utilizar el control deslizante para filtrar las conexiones que no son fuertes.  
  
     **Slider**  
     El **control deslizante** le permite controlar la importancia de las relaciones que se muestran en el diagrama de red de dependencias.  
  
     Cada nodo del gráfico representa un estado. Una flecha representa una transición entre dos estados y la probabilidad asociada a la transición. Para reducir el número de nodos del gráfico, mueva la barra del control deslizante hacia arriba.  
  
     Para aumentar el número de nodos del gráfico, mueva la barra del control deslizante hacia abajo.  
  
     **Agregar elementos**  
     Se abre el **seleccionar nodos que se representarán** cuadro de diálogo para que pueda seleccionar nuevos nodos para agregar al gráfico.  
  
4.  Puede hacer que los gráficos sean todo lo sencillos o elaborados que desee, así como agregar anotaciones mientras está conectado al modelo.  
  
     [art placeholder]  
  
> [!WARNING]  
>  El resaltado de los nodos dependientes y otras opciones del menú contextual que estaban disponibles en versiones anteriores de los complementos no funcionan en Office 2013.  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de diagramas de minería de datos de Visio &#40;complementos de minería de datos de SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
