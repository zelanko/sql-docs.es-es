---
title: Pestaña distinción del clúster (Visor de modelos de minería de datos) de clústeres de secuencia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.sequenceclustering.discrimination.f1
ms.assetid: 7dd16479-2633-4f4b-83bf-cf55972a2241
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d4debc43286ffb3fe4f87115ed15e9b4c3f74b06
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187152"
---
# <a name="sequence-clustering-cluster-discrimination-tab-mining-model-viewer"></a>Pestaña Distinción del clúster de agrupación en clústeres de secuencia (Visor de modelos de minería de datos)
  La pestaña  **Distinción del clúster** del **Visor de agrupación en clústeres de secuencia de Microsoft** compara los clústeres seleccionados de un modelo de agrupación en clústeres de secuencia.  
  
 Utilice esta vista de un modelo de agrupación en clústeres de secuencia para comparar dos clústeres y ver qué estados y transiciones son diferentes.  
  
 **Para más información:** [Algoritmo de clústeres de secuencia de Microsoft](data-mining/microsoft-sequence-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
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
  
 **Puntuaciones de distinción para \<clúster 1 > y \<clúster 2 >**  
 Este gráfico proporciona una comparación detallada de los clústeres seleccionados. En general, un modelo de agrupación en clústeres raramente asigna estados o valores exclusivamente a un único clúster. Por consiguiente, el visor solo indica que un determinado atributo o estado *favorece* un determinado clúster.  
  
 En general, algún clúster podría contener más de un estado: por ejemplo, un estado común podría ser la compra de una Botella de agua y de un Portabotellas secuencialmente. Sin embargo, la secuencia se podría encontrar en otros clústeres que tengan características de definición más importantes. Por ejemplo, otro clúster podría estar caracterizado más firmemente por unos tiempos de transacción muy cortos, y un análisis revelaría que los elementos [Water Bottle y Water] normalmente se agruparían en este clúster, pero no siempre.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Variables**|Un atributo del modelo de minería de datos.|  
|**Valores**|Un estado del atributo que se incluye en **Variables**.|  
|**Favorece \<clúster 1 >**|Contiene una barra sombreada que indica con qué intensidad el atributo y el estado se incluyen en **Variables** y **Valor** a favor del clúster seleccionado en **Clúster 1**.|  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
