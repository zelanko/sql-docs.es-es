---
title: Tutorial (complementos de minería de datos) del diagrama de árbol de decisión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- shapes, data mining
- diagram, decision tree
- Visio shapes, decision tree
- decision tree [data mining]
ms.assetid: 9566f6a2-c750-4125-ba5e-42c7251a78c7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55bdeb41ed62fd727a6e5eb637734a67d21660fe
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391238"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>Tutorial de diagrama de árbol de decisión (complementos de minería de datos)
  Si ha creado un modelo de árbol de decisión, podrá crear un diagrama personalizado en Visio con la forma Árbol de decisión o la forma Red de dependencias. En este tema se describe las personalizaciones que puede realizar con el **árbol de decisión** forma y estos controles:  
  
-   Representar los controles del diagrama de árbol de decisión  
  
     Estas opciones forman parte de la **Asistente para crear el árbol de decisión** que se inicia cuando se coloca una forma en el área de trabajo de Visio.  
  
-   **Diseño de minería de datos** barra de herramientas  
  
     Estas opciones se agregan al área de trabajo de Visio con el fin de ayudarle a interactuar con la forma.  
  
## <a name="build-a-decision-tree-diagram"></a>Generar un diagrama de árbol de decisión  
 Coloque la forma de árbol de decisión en la página de Visio para iniciar el **Asistente para la forma de Visio de árbol de decisión** y establecer las opciones del diagrama.  
  
#### <a name="use-the-decision-tree-wizard"></a>Usar el Asistente para árbol de decisión  
  
1.  Si no ve **formas de minería de datos de Microsoft** en el **formas** lista, haga clic en **más formas**, seleccione **Abrir galería de símbolos**y abra el plantilla de la ubicación de instalación predeterminada.  
  
     \<unidad >: \Program files (x85) \Microsoft SQL Server 2012 DM Add-Ins  
  
2.  Arrastre el **árbol de decisión** forma en la página.  
  
3.  En la página principal de la **Asistente para la forma de Visio de árbol de decisión**, haga clic en **siguiente**.  
  
4.  En el **seleccionar un origen de datos** página de la **Asistente para clúster**, elegir una conexión a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor que contiene el modelo que desea visualizar.  
  
5.  Seleccione un modelo de minería de datos adecuado y haga clic en **siguiente**.  
  
     Este tipo de diagrama admite modelos creados mediante el algoritmo de árboles de decisión o de regresión lineal.  
  
6.  En el **seleccionar el árbol de decisión** página, elija un árbol individual para mostrar.  
  
     Un árbol modela las interacciones que conducen a un resultado determinado que haya modelado; por lo tanto, incluso si el modelo contiene varios resultados, puede mostrar un único árbol a la vez.  
  
7.  En el **seleccionar el árbol de decisión** cuadro de diálogo, también puede establecer estas opciones de presentación:  
  
     **Profundidad máxima de representación**  
     Esta opción se usa para controlar la cantidad de nodos que se van a mostrar.  
  
     Un árbol de decisión puede ser muy profundo y crear un diagrama que no cabe en la página. Este control se usa para centrarse en los nodos del extremo izquierdo, que son los más importantes.  
  
     El valor predeterminado es tres niveles de nodos.  
  
     **Seleccione un color y mostrar el texto de valores**  
     Elija el color que representará cada uno de los resultados. Si no especifica colores, se generan automáticamente mediante los colores del tema de vídeo.  
  
8.  Haga clic en **avanzadas** para personalizar las opciones siguientes para cada uno de los nodos en el diagrama de árbol de decisión.  
  
     **Variable de sombreado** y **estado**  
     Elija el resultado de destino que desea mostrar en el diagrama de árbol.  
  
     **Mostrar histograma**  
     Agrega un gráfico a cada nodo que muestra las reglas que definen el nodo.  
  
     **Mostrar etiqueta**  
     Agrega nombres de columna al histograma.  
  
     **Mostrar la probabilidad**  
     Muestra la probabilidad de cada valor.  
  
     **Mostrar compatibilidad**  
     Muestra el soporte de cada valor.  
  
     **Mostrar pie**  
     Agrega un pie de página que reúne a todos los valores mostrados.  
  
     **Mostrar encabezado**  
     Agrega encabezados de columna.  
  
     **Mostrar estados con compatibilidad cero**  
     Permite mostrar los valores que faltan.  
  
9. Haga clic en **finalizar** para crear el gráfico.  
  
    > [!WARNING]  
    >  En algunos entornos, los conectores del gráfico podrían producir errores de representación en Office 2013.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar y modificar el diagrama finalizado  
 Después de haber completado la **Asistente para la forma de Visio de árbol de decisión**, Visio crea un diagrama de árbol en la página que muestra gráficamente las reglas que conducen al resultado pronosticado.  
  
 Puede seguir modificando la forma si usa los controles siguientes para diagramas de árbol de decisión:  
  
#### <a name="using-the-decision-tree-option-menus"></a>Usar los menús de opción del árbol de decisión  
  
1.  Haga clic en el **Add-Ins** la cinta de opciones y, a continuación, mostrar una de las barras de herramientas personalizados utilizados para trabajar con diagramas de minería de datos:  
  
     **Diseño**  
     Optimiza la organización del árbol para que se ajuste a la página actual.  
  
     **Cambiar el tamaño de página**  
     Este control se ha diseñado para la versiones anteriores de HTML. Use la página de Visio, cambiar el tamaño de los controles en su lugar,  
  
     **Descripción**  
     Cuando se selecciona un nodo del árbol, haga clic en esta opción para mostrar los detalles sobre los casos del nodo.  
  
2.  Use la **rediseñar página** opción en el Visio **diseño** cinta de opciones para experimentar con distintos diseños de árbol.  
  
3.  Use la **conectores** opción el **diseño** tab para cambiar los conectores usan entre nodos en el árbol.  
  
4.  Use la **panorámica y Zoom** controlar, en el **panel de tareas** área de la Visio **vista** cinta de opciones para centrarse en un área determinada del diagrama.  
  
5.  Haga clic con el botón secundario en cualquier nodo del árbol y elija en el menú contextual las opciones específicas de los diagramas de árbol de decisión:  
  
     **Mejorar el diseño de página**  
     Distribuye uniformemente los nodos en la página y ajusta la vista de la misma para que se vean todos ellos.  
  
     **Mover a los elementos secundarios a nueva página**  
     Mueve los elementos secundarios del nodo seleccionado actualmente a una página nueva.  
  
     **Contraer nodos secundarios**  
     Oculta los elementos secundarios del nodo seleccionado actualmente.  
  
     **Expanda los nodos secundarios**  
     Muestra los nodos secundarios del nodo seleccionado actualmente.  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas de diagramas de minería de datos de Visio &#40;complementos de minería de datos de SQL Server&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
