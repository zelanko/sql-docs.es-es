---
title: Pestaña transición del clúster de clústeres de secuencia (visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.transition.f1
ms.assetid: 40aef457-d69f-4905-a2d3-924c37bd3d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a236805ac047b351aa49c2486b8acac84818017
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069079"
---
# <a name="sequence-clustering-cluster-transition-tab-mining-model-viewer"></a>Pestaña Transiciones de estado de agrupación en clústeres de secuencia (Visor de modelos de minería de datos)
  La pestaña **Transiciones de estado** del **Visor de clústeres de secuencia de Microsoft** muestra con mayor detalle las transiciones entre los pares de atributo-valor o los estados, en el clúster seleccionado.  
  
 Utilice esta vista de un modelo de agrupación en clústeres de secuencia para ver los patrones. En el diagrama, un vínculo representa la probabilidad de una transición, y un nodo representa un estado de secuencia.  
  
 **Para más información:** [Algoritmo de clústeres de secuencia de Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor que desee usar para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado o el **Visor de árbol de contenido genérico de Microsoft**. También puede utilizar visores de complemento si están disponibles.  
  
 **Acercar**  
 Amplíe el diagrama, para ver los estados mejor.  
  
 **Alejar**  
 Aleje el diagrama, para obtener una vista general de los estados del clúster.  
  
 **Copiar vista del gráfico**  
 Copie la sección visible del diagrama en el portapapeles.  
  
 **Copiar todo el gráfico**  
 Copie el diagrama completo en el portapapeles.  
  
 **Clúster**  
 Elija un clúster para mostrarlo en el visor. De forma predeterminada, está seleccionada la opción **Población (Todo)** , lo que significa que los estados y transiciones de todo el modelo se incluyen en el gráfico. Al elegir un clúster determinado, se muestran solo los estados y transiciones que pertenecen a ese clúster.  
  
 **Sugerencia:** Puede cambiar el nombre de los clústeres mediante la pestaña **Diagrama del clúster** . Simplemente seleccione un clúster, haga clic con el botón derecho y seleccione **cambiar nombre**. Cambiar el nombre de los clústeres por una etiqueta más descriptiva facilita la comparación de los clústeres en la pestaña **Transiciones de estado** .  
  
 **Mostrar etiquetas de bordes**  
 Seleccione esta opción para mostrar números en cada borde del gráfico que denote la probabilidad de la transición.  
  
 **Vínculos**  
 Utilice el control deslizante para controlar el número de estados y transiciones que se muestran en el gráfico. Si baja el control deslizante solo se muestran los estados y transiciones con la probabilidad más alta.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
