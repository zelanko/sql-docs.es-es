---
title: Pestaña distinción del clúster de clústeres de secuencia (visor de modelos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
author: minewiskan
ms.author: owend
ms.openlocfilehash: 705fb7bfd5fe8df27d39f81ed648f6406b6aa8dd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940746"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>Pestaña Distinción del clúster de agrupación en clústeres de secuencia (Visor de modelos de minería de datos)
  La pestaña  **Distinción del clúster** del **Visor de agrupación en clústeres de secuencia de Microsoft** compara los clústeres seleccionados de un modelo de agrupación en clústeres de secuencia.  
  
 Utilice esta vista de un modelo de agrupación en clústeres de secuencia para comparar dos clústeres y ver qué estados y transiciones son diferentes.  
  
 **Para más información:** [Algoritmo de clústeres de secuencia de Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija esta opción para ver un modelo de minería de datos que se encuentra en la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor que desee usar para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado o el **Visor de árbol de contenido genérico de Microsoft**. También puede utilizar visores de complemento si están disponibles.  
  
 **Clúster 1**  
 Seleccione un clúster de los del modelo.  
  
 **Clúster 2**  
 Seleccione un segundo clúster del modelo de minería de datos para compararlo con el **Clúster 1**.  
  
 Si no selecciona otro clúster, de forma predeterminada el clúster seleccionado se compara con su complemento, es decir, con todos los casos del modelo que no están en el Clúster 1.  
  
 **Puntuaciones de distinción para \<cluster 1> y\<cluster 2>**  
 Este gráfico proporciona una comparación detallada de los clústeres seleccionados. En general, un modelo de agrupación en clústeres raramente asigna estados o valores exclusivamente a un único clúster. Por consiguiente, el visor solo indica que un determinado atributo o estado *favorece* un determinado clúster.  
  
 En general, algún clúster podría contener más de un estado: por ejemplo, un estado común podría ser la compra de una Botella de agua y de un Portabotellas secuencialmente. Sin embargo, la secuencia se podría encontrar en otros clústeres que tengan características de definición más importantes. Por ejemplo, otro clúster podría estar caracterizado más firmemente por unos tiempos de transacción muy cortos, y un análisis revelaría que los elementos [Water Bottle y Water] normalmente se agruparían en este clúster, pero no siempre.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Variables**|Un atributo del modelo de minería de datos.|  
|**Valores**|Un estado del atributo que se incluye en **Variables**.|  
|**Favorece\<cluster 1>**|Contiene una barra sombreada que indica con qué intensidad el atributo y el estado se incluyen en **Variables** y **Valor** a favor del clúster seleccionado en **Clúster 1**.|  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
