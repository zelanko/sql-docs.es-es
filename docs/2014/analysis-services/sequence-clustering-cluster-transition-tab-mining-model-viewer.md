---
title: Pestaña transiciones de estado (Visor de modelos de minería de datos) de clústeres de secuencia | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.transition.f1
ms.assetid: 40aef457-d69f-4905-a2d3-924c37bd3d97
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d9895e00405c4ebe6bc684c3c2b3acc4e2704478
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109029"
---
# <a name="sequence-clustering-cluster-transition-tab-mining-model-viewer"></a>Pestaña Transiciones de estado de agrupación en clústeres de secuencia (Visor de modelos de minería de datos)
  La pestaña **Transiciones de estado** del **Visor de clústeres de secuencia de Microsoft** muestra con mayor detalle las transiciones entre los pares de atributo-valor o los estados, en el clúster seleccionado.  
  
 Utilice esta vista de un modelo de agrupación en clústeres de secuencia para ver los patrones. En el diagrama, un vínculo representa la probabilidad de una transición, y un nodo representa un estado de secuencia.  
  
 **Para más información:** [Algoritmo de clústeres de secuencia de Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
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
  
 **Cluster**  
 Elija un clúster para mostrarlo en el visor. De forma predeterminada, está seleccionada la opción **Población (Todo)** , lo que significa que los estados y transiciones de todo el modelo se incluyen en el gráfico. Al elegir un clúster determinado, se muestran solo los estados y transiciones que pertenecen a ese clúster.  
  
 **Sugerencia:** puede cambiar el nombre de los clústeres utilizando la pestaña **Diagrama del clúster** . Tan solo tiene que seleccionar un clúster, hacer clic con el botón derecho y elegir **Cambiar nombre**. Cambiar el nombre de los clústeres por una etiqueta más descriptiva facilita la comparación de los clústeres en la pestaña **Transiciones de estado** .  
  
 **Mostrar etiquetas de bordes**  
 Seleccione esta opción para mostrar números en cada borde del gráfico que denote la probabilidad de la transición.  
  
 **Vínculos**  
 Utilice el control deslizante para controlar el número de estados y transiciones que se muestran en el gráfico. Si baja el control deslizante solo se muestran los estados y transiciones con la probabilidad más alta.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  