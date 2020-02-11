---
title: Tutorial del diagrama de árbol de decisión (complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
ms.openlocfilehash: ef951825144f381ab37a83526ec96321fe43cfec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082279"
---
# <a name="decision-tree-diagram-walkthrough--data-mining-add-ins"></a>Tutorial del diagrama de árbol de decisión (complementos de minería de datos)
  Si ha creado un modelo de árbol de decisión, podrá crear un diagrama personalizado en Visio con la forma Árbol de decisión o la forma Red de dependencias. En este tema se describen las personalizaciones que puede realizar con la forma **árbol de decisión** y estos controles:  
  
-   Representar los controles del diagrama de árbol de decisión  
  
     Estas opciones forman parte del **Asistente para árbol de decisión** que se inicia cuando se coloca una forma en el área de trabajo de Visio.  
  
-   Barra de herramientas de **diseño de minería de datos**  
  
     Estas opciones se agregan al área de trabajo de Visio con el fin de ayudarle a interactuar con la forma.  
  
## <a name="build-a-decision-tree-diagram"></a>Generar un diagrama de árbol de decisión  
 Coloque la forma árbol de decisión en la página de Visio para iniciar el **Asistente para crear formas árbol de decisión de Visio** y establecer las opciones del diagrama.  
  
#### <a name="use-the-decision-tree-wizard"></a>Usar el Asistente para árbol de decisión  
  
1.  Si no ve formas de **minería de datos de Microsoft** en la lista **formas** , haga clic en **más formas**, seleccione **Abrir Galería de símbolos**y abra la plantilla desde la ubicación de instalación predeterminada.  
  
     \<> de unidad: \Archivos de programa (x85) \Microsoft SQL Server 2012 DM-ins  
  
2.  Arrastre la forma **árbol de decisión** hasta la página.  
  
3.  En la página de bienvenida del **Asistente para crear formas árbol de decisión de Visio**, haga clic en **siguiente**.  
  
4.  En la página **seleccionar un origen de datos** del **Asistente para clúster**, elija una conexión a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] un servidor que tenga el modelo que desea visualizar.  
  
5.  Seleccione un modelo de minería de datos adecuado y haga clic en **siguiente**.  
  
     Este tipo de diagrama admite modelos creados mediante el algoritmo de árboles de decisión o de regresión lineal.  
  
6.  En la página **Seleccionar árbol de decisión** , elija un árbol individual para mostrar.  
  
     Un árbol modela las interacciones que conducen a un resultado determinado que se ha modelado. por lo tanto, incluso si el modelo contiene varios resultados, solo puede mostrar un árbol cada vez.  
  
7.  En el cuadro de diálogo **Seleccionar árbol de decisión** , también puede establecer estas opciones de representación:  
  
     **Profundidad máxima de representación**  
     Esta opción se usa para controlar la cantidad de nodos que se van a mostrar.  
  
     Un árbol de decisión puede ser muy profundo y crear un diagrama que no cabe en la página. Este control se usa para centrarse en los nodos del extremo izquierdo, que son los más importantes.  
  
     El valor predeterminado es tres niveles de nodos.  
  
     **Seleccionar un color y un texto para los valores**  
     Elija el color que representará cada uno de los resultados. Si no especifica colores, se generan automáticamente mediante los colores del tema de vídeo.  
  
8.  Haga clic en **avanzadas** para personalizar las siguientes opciones para cada uno de los nodos del diagrama de árbol de decisión.  
  
     **Variable de sombreado** y **Estado**  
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
  
9. Haga clic en **Finalizar** para crear el gráfico.  
  
    > [!WARNING]  
    >  En algunos entornos, los conectores del gráfico podrían producir errores de representación en Office 2013.  
  
## <a name="explore-and-modify-the-finished-diagram"></a>Explorar y modificar el diagrama finalizado  
 Después de haber completado el **Asistente para crear formas árbol de decisión de Visio**, Visio crea un diagrama de árbol en la página que muestra gráficamente las reglas que conducen al resultado predicho.  
  
 Puede seguir modificando la forma si usa los controles siguientes para diagramas de árbol de decisión:  
  
#### <a name="using-the-decision-tree-option-menus"></a>Usar los menús de opción del árbol de decisión  
  
1.  Haga clic en la cinta de opciones de **Complementos** y, a continuación, muestre una de las barras de herramientas personalizadas que se usan para trabajar con diagramas de minería de datos:  
  
     **Diseño**  
     Optimiza la organización del árbol para que se ajuste a la página actual.  
  
     **Cambiar tamaño de página**  
     Este control se ha diseñado para la versiones anteriores de HTML. En su lugar, use la página de Visio para cambiar el tamaño de los controles.  
  
     **Descripción**  
     Cuando se selecciona un nodo del árbol, haga clic en esta opción para mostrar los detalles sobre los casos del nodo.  
  
2.  Use la opción de **Página rediseño** de la cinta de opciones **diseño** de Visio para experimentar con distintos diseños de árbol.  
  
3.  Use la opción **conectores** en la pestaña **diseño** para cambiar los conectores usados entre los nodos del árbol.  
  
4.  Use el control **panorámica y zoom** , en el área del **Panel de tareas** de la cinta de opciones **vista** de Visio, para centrarse en un área determinada del diagrama.  
  
5.  Haga clic con el botón secundario en cualquier nodo del árbol y elija en el menú contextual las opciones específicas de los diagramas de árbol de decisión:  
  
     **Mejorar diseño de página**  
     Distribuye uniformemente los nodos en la página y ajusta la vista de la misma para que se vean todos ellos.  
  
     **Mover secundarios a nueva página**  
     Mueve los elementos secundarios del nodo seleccionado actualmente a una página nueva.  
  
     **Contraer nodos secundarios**  
     Oculta los elementos secundarios del nodo seleccionado actualmente.  
  
     **Expandir nodos secundarios**  
     Muestra los nodos secundarios del nodo seleccionado actualmente.  
  
## <a name="see-also"></a>Consulte también  
 [Solucionar problemas de diagramas de minería de datos de Visio &#40;SQL Server complementos de minería de datos&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
