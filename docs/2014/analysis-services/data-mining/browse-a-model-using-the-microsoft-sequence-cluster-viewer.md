---
title: Examinar un modelo usando el visor de clústeres de secuencia de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Sequence Cluster Viewer
- clusters [Analysis Services]
- data mining [Analysis Services], sequences
- discrimination [Analysis Services]
- mining model content, viewing
- mining models [Analysis Services], sequences
- Microsoft Sequence Cluster Viewer
- sequence [Analysis Services]
- transitions [Analysis Services]
ms.assetid: 3ada00aa-da9e-488a-9f53-c3e188f81f84
author: minewiskan
ms.author: owend
ms.openlocfilehash: 5e7262beef3e9d64a488e255fe5fd9f1b79a8837
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525285"
---
# <a name="browse-a-model-using-the-microsoft-sequence-cluster-viewer"></a>Examinar un modelo usando el Visor de clústeres de Microsoft
  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] visor de clústeres de secuencia de en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo de clústeres de secuencia de. El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de clústeres de secuencia que se utiliza para explorar datos que contienen eventos que se pueden vincular siguiendo rutas o *secuencias*. Para más información sobre este algoritmo, vea [Algoritmo de clústeres de secuencia de Microsoft](microsoft-sequence-clustering-algorithm.md).  
  
> [!NOTE]  
>  Para ver información detallada sobre las ecuaciones utilizadas en el modelo y los modelos que se detectaron, utilice el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).  
  
> [!NOTE]  
>  El visor de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] proporciona funcionalidad y opciones similares a las del visor de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener más información, vea [Examinar un modelo usando el Visor de clústeres de Microsoft](browse-a-model-using-the-microsoft-cluster-viewer.md).  
  
##  <a name="viewer-tabs"></a><a name="BKMK_ViewerTabs"></a>Pestañas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ofrece las siguientes pestañas para utilizarlas con el fin de explorar modelos de minería de datos de agrupación en clústeres de secuencia:  
  
-   [Diagrama del clúster](#BKMK_Diagram)  
  
-   [Perfiles del clúster](#BKMK_Profile)  
  
-   [Características del clúster](#BKMK_Characteristics)  
  
-   [Distinción del clúster](#BKMK_Discrimination)  
  
-   [Transiciones de estado](#BKMK_Transitions)  
  
###  <a name="cluster-diagram"></a><a name="BKMK_Diagram"></a>Diagrama del clúster  
 La pestaña **Diagrama del clúster** del Visor de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] muestra todos los clústeres de un modelo de minería de datos. El sombreado de la línea que conecta un clúster con otro representa la importancia de la similitud de los clústeres. Si el sombreado es claro o inexistente, los clústeres no son muy similares. A medida que la línea se va oscureciendo, va aumentando la similitud de los vínculos. Puede ajustar el número de líneas que muestra el visor ajustando el control deslizante situado a la derecha de los clústeres. Si desplaza el control deslizante hacia abajo, sólo se verán los vínculos más similares.  
  
 De forma predeterminada, el sombreado representa el llenado del clúster. Mediante el uso de las opciones de **sombreado** y **Estado** , puede seleccionar el par de atributo y estado que representa el sombreado. Cuanto más oscuro sea el sombreado, mayor será la distribución del atributo para un estado concreto. La distribución disminuye a medida que se aclara el sombreado.  
  
 Para cambiar el nombre de un clúster, haga clic con el botón derecho en su nodo y seleccione **Cambiar nombre de clúster**. El nuevo nombre se mantiene en el servidor.  
  
 Para copiar la sección visible del diagrama al Portapapeles, haga clic en **Copiar vista del gráfico**. Para copiar el diagrama completo, haga clic en **Copiar todo el gráfico**. También puede acercar o alejar el diagrama con las opciones **Acercar** y **Alejar**o ajustar el diagrama a la pantalla con **Ajustar diagrama a la ventana**.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="cluster-profiles"></a><a name="BKMK_Profile"></a>Perfiles del clúster  
 La pestaña **Perfiles del clúster** proporciona una vista general de los clústeres que crea el algoritmo del modelo. Cada columna que sigue a la columna **Llenado** en la cuadrícula representa un clúster que el modelo ha descubierto. La \<attribute> fila. samples representa diferentes secuencias de datos que existen en el clúster y la \<attribute> fila describe todos los elementos que contiene el clúster y su distribución general.  
  
 La opción **Barras de histograma** controla el número de barras que están visibles en el histograma. Si hay más barras de las que elige que se muestren, se retienen las de mayor importancia y las restantes se agrupan en un depósito gris.  
  
 Puede cambiar los nombres predeterminados de los clústeres para hacerlos más descriptivos. Puede cambiar el nombre de un clúster haciendo clic con el botón derecho en su encabezado de columna y seleccionando **Cambiar nombre de clúster**. Puede ocultar clústeres seleccionado **Ocultar columna**y arrastrar columnas para volver a ordenarlas en el visor.  
  
 Para abrir una ventana que ofrezca una vista mayor y más detallada de los clústeres, haga doble clic en una celda de la columna **Estados** o en un histograma del visor.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="cluster-characteristics"></a><a name="BKMK_Characteristics"></a>Características del clúster  
 Para utilizar la pestaña **Características del clúster** , seleccione un clúster de la lista **Clúster** . Tras seleccionar un clúster, puede examinar las características que lo componen. Los atributos que contiene el clúster se enumeran en las columnas **Variables** ; el estado del atributo se indica en la columna **Valores** . Los estados del atributo se enumeran por orden de importancia, según la probabilidad que tienen de aparecer en el clúster. La probabilidad se muestra en la columna **Probabilidad** .  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="cluster-discrimination"></a><a name="BKMK_Discrimination"></a>Distinción del clúster  
 Puede utilizar la pestaña **Distinción del clúster** para comparar los atributos de dos clústeres con el fin de determinar el modo en que los elementos de una secuencia favorecen a uno u otro. Utilice las listas **Clúster 1** y **Clúster 2** para seleccionar los clústeres que desea comparar. El visor determina las diferencias más importantes entre los clústeres y muestra los estados de atributo asociados con las diferencias por orden de importancia. Una barra a la derecha del atributo muestra el clúster que favorece el estado; el tamaño de la barra muestra la intensidad con la que lo favorece.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="cluster-transitions"></a><a name="BKMK_Transitions"></a>Transiciones del clúster  
 Si selecciona un clúster en la pestaña **Transiciones de estado** , puede examinar las transiciones entre los estados de secuencia del clúster seleccionado. Cada nodo del visor representa un estado de la columna de secuencia. Una flecha representa una transición entre dos estados y la probabilidad asociada a la transición. Si la transición vuelve al nodo original, una flecha puede apuntar al nodo original.  
  
 Una flecha que se origina en un punto representa la probabilidad de que el nodo sea el inicio de la secuencia. Un borde final que conduce a un valor nulo representa la probabilidad de que el nodo sea el final de la secuencia.  
  
 Puede filtrar el borde de los nodos utilizando el control deslizante situado a la izquierda de la pestaña.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Consulte también  
 [Tareas y procedimientos del visor de modelos de minería de datos](mining-model-viewer-tasks-and-how-tos.md)   
 [Tareas y procedimientos del visor de modelos de minería de datos](mining-model-viewer-tasks-and-how-tos.md)   
 [Algoritmo de clústeres de secuencia de Microsoft](microsoft-sequence-clustering-algorithm.md)   
 [Herramientas de minería de datos](data-mining-tools.md)   
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)   
 [Examinar un modelo usando el Visor de clústeres de Microsoft](browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
  
