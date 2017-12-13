---
title: "Examinar un modelo usando el Visor de clústeres de Microsoft | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clusters [Analysis Services]
- discrimination [Analysis Services]
- names [Analysis Services], clusters
- Microsoft Cluster Viewer
- mining model content, viewing
- comparing clusters
- viewing clusters
- displaying clusters
- data mining [Analysis Services], clusters
- Cluster Viewer [Analysis Services]
- mining models [Analysis Services], clusters
ms.assetid: 591fe30b-d88f-4a71-94d4-4a3907fc275d
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 78190bb150a0cb1df68722c0ed602c88f413be9a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="browse-a-model-using-the-microsoft-cluster-viewer"></a>Examinar un modelo usando el Visor de clústeres de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]El [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visor de clústeres en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los modelos de minería de datos que se generan con el [!INCLUDE[msCoName](../../includes/msconame-md.md)] algoritmo de clústeres. El algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de segmentación que se utiliza para explorar datos con el fin de identificar anomalías en ellos y crear predicciones. Para más información acerca de este algoritmo, consulte [Microsoft Clustering Algorithm](../../analysis-services/data-mining/microsoft-clustering-algorithm.md).  
  
> [!NOTE]  
>  Para ver información detallada sobre las ecuaciones utilizadas en el modelo y los modelos que se detectaron, utilice el Visor de árbol de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md) o [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
##  <a name="BKMK_ViewerTabs"></a> Fichas del visor  
 Cuando se explora un modelo de minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el modelo aparece en la pestaña **Visor de modelos de minería de datos** del visor del diseñador de minería de datos apropiado para el modelo. El Visor de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ofrece las siguientes pestañas para la exploración de modelos de minería de datos de agrupación en clústeres:  
  
-   [Diagrama del clúster](#BKMK_Diagram)  
  
-   [Perfiles del clúster](#BKMK_Profile)  
  
-   [Características del clúster](#BKMK_Characteristics)  
  
-   [Distinción del clúster](#BKMK_Discrimination)  
  
###  <a name="BKMK_Diagram"></a> Diagrama del clúster  
 La pestaña **Diagrama del clúster** del Visor de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] muestra todos los clústeres de un modelo de minería de datos. El sombreado de la línea que conecta un clúster con otro representa la importancia de la similitud de los clústeres. Si el sombreado es claro o inexistente, los clústeres no son muy similares. A medida que la línea se va oscureciendo, va aumentando la similitud de los vínculos. Puede ajustar el número de líneas que muestra el visor ajustando el control deslizante situado a la derecha de los clústeres. Si desplaza el control deslizante hacia abajo, sólo se verán los vínculos más similares.  
  
 De forma predeterminada, el sombreado representa el llenado del clúster. Mediante las opciones **Variable de sombreado** y **Estado** , puede seleccionar el par de atributo y estado que representa el sombreado. Cuanto más oscuro sea el sombreado, mayor será la distribución del atributo para un estado concreto. La distribución disminuye a medida que se aclara el sombreado.  
  
 Para cambiar el nombre de un clúster, haga clic con el botón derecho en su nodo y seleccione **Cambiar nombre de clúster**. El nuevo nombre se mantiene en el servidor.  
  
 Para copiar la sección visible del diagrama al Portapapeles, haga clic en **Copiar vista del gráfico**. Para copiar el diagrama completo, haga clic en **Copiar todo el gráfico**. También puede acercar o alejar el diagrama con las opciones **Acercar** y **Alejar**o ajustar el diagrama a la pantalla con **Ajustar diagrama a la ventana**.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> Perfiles del clúster  
 La pestaña **Perfiles del clúster** proporciona una vista general de los clústeres que crea el algoritmo en el modelo. Esta vista muestra cada atributo, junto con su distribución en cada clúster. Un recuadro informativo por cada celda muestra las estadísticas de la distribución y otro por cada encabezado de columna muestra el llenado del clúster. Los atributos discretos se muestran como barras de color y los atributos continuos se muestran como un gráfico en forma de rombo que representa la media y la desviación estándar de cada cluster. La opción **Barras de histograma** controla el número de barras que están visibles en el histograma. Si hay más barras de las que elige que se muestren, se retienen las de mayor importancia y las restantes se agrupan en un depósito gris.  
  
 Puede cambiar los nombres predeterminados de los clústeres para hacerlos más descriptivos. Puede cambiar el nombre de un clúster haciendo clic con el botón derecho en su encabezado de columna y seleccionando **Cambiar nombre de clúster**. También puede ocultar clústeres seleccionando **Ocultar columna**.  
  
 Para abrir una ventana que ofrezca una vista mayor y más detallada de los clústeres, haga doble clic en una celda de la columna **Estados** o en un histograma del visor.  
  
 Haga clic en un encabezado de columna para ordenar los atributos por orden de importancia respecto a ese clúster. También puede arrastrar las columnas para volver a ordenarlas en el visor.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> Características del clúster  
 Para utilizar la pestaña **Características del clúster** , seleccione un clúster de la lista **Clúster** . Tras seleccionar un clúster, puede examinar las características que lo componen. Los atributos que contiene el clúster se enumeran en las columnas **Variables** ; el estado del atributo se indica en la columna **Valores** . Los estados del atributo se enumeran por orden de importancia, según la probabilidad que tienen de aparecer en el clúster. La probabilidad se muestra en la columna **Probabilidad** .  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> Distinción del clúster  
 Puede utilizar la ficha **Distinción del clúster** para comparar los atributos de dos clústeres. Utilice las listas **Clúster 1** y **Clúster 2** para seleccionar los clústeres que desea comparar. El visor determina las diferencias más importantes entre los clústeres y muestra los estados de atributo asociados con las diferencias por orden de importancia. Una barra a la derecha del atributo muestra el clúster que favorece el estado; el tamaño de la barra muestra la intensidad con la que lo favorece.  
  
 [Volver al principio](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>Vea también  
 [Microsoft Clustering Algorithm](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)   
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
