---
title: Pestaña distinción del (Visor de modelos de minería de datos) del clúster | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.clustering.discrimination.f1
ms.assetid: ae7cfff7-ab1c-4cf5-9a91-97b21d15d85f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc00f10403f748db0802f288ca66e6582429155c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075065"
---
# <a name="cluster-discrimination-tab-mining-model-viewer"></a>Pestaña Distinción del clúster (Visor de modelos de minería de datos)
  Utilice la pestaña **Distinción del clúster** para comparar dos clústeres que existan en un modelo de agrupación en clústeres. Puede ver cómo las diferentes combinaciones de atributos y valores se representan dentro de los clústeres.  
  
 **Para obtener más información:** [Algoritmo de clústeres de Microsoft](data-mining/microsoft-clustering-algorithm.md), [Examinar un modelo usando el Visor de clústeres de Microsoft](data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
## <a name="options"></a>Opciones  
 **Actualizar el contenido del Visor**  
 Vuelva a cargar el modelo de minería de datos en el visor.  
  
 **Modelo de minería de datos**  
 Elija un modelo de minería de datos de los de la estructura de minería de datos actual. El modelo de minería de datos se abrirá en el visor asociado.  
  
 **Visor**  
 Elija un visor para explorar el modelo de minería de datos seleccionado. Puede utilizar el visor personalizado de los modelos de agrupación en clústeres o el Visor de contenido de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] . También puede utilizar visores de complemento si están disponibles.  
  
 **Clúster 1**  
 Seleccione un clúster, para que pueda compararlo con otro clúster.  
  
 **Clúster 2**  
 Seleccione un segundo clúster de la lista de clústeres del modelo de minería de datos para compararlo con el **Clúster 1**. También puede comparar un clúster con su complemento, es decir, con todos los casos del modelo excepto los del clúster seleccionado.  
  
 **Puntuaciones de distinción para \<clúster 1 > y \<clúster 2 >**  
 Las columnas del gráfico proporcionan información sobre cómo se relaciona cada par de atributo-valor con los dos clústeres seleccionados.  
  
|||  
|-|-|  
|**Variables**|Un atributo del modelo de minería de datos.|  
|**Valores**|Un valor del atributo seleccionado en **Variables**.|  
|**Favorece \<clúster 1 >**|El gráfico de barras de la izquierda representa la probabilidad de que el par de atributo-valor seleccionado sea representativo del clúster seleccionado en **Clúster 1**. Puede detener el mouse sobre la barra ver el valor, representado como un porcentaje. Tenga en cuenta que aun cuando el valor sea cero, no significa necesariamente que el par de atributo-valor falte en el clúster, solo que la distribución favorece más a un clúster sobre el otro.|  
|**Favorece \<clúster 2 >**|El gráfico de barras de la derecha representa la probabilidad de que el par de atributo-valor seleccionado sea representativo del clúster seleccionado en **Clúster 2**.|  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Visores de modelos de minería de datos &#40;Diseñador de modelos de minería de datos&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Visores de modelos de minería de datos](data-mining/data-mining-model-viewers.md)  
  
  
