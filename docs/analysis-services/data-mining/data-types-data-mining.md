---
title: "Tipos de datos (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
caps.latest.revision: "47"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7e5d09435546cf0605bb7b70a685021612fd2f9b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="data-types-data-mining"></a>Tipos de datos (minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Cuando se crea un modelo de minería de datos o una estructura de minería de datos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], debe definir los tipos de datos para cada una de las columnas de la estructura de minería de datos. Los tipos de datos indican al motor de análisis si los datos del origen de datos son numéricos o de texto y cómo deben procesarse los datos. Por ejemplo, si el origen de datos contiene datos numéricos, puede especificar si los números deben tratarse como enteros o utilizando posiciones decimales.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite los tipos de datos siguientes para las columnas de estructura de minería:  
  
|Tipo de datos|Tipos de contenido admitidos|  
|---------------|-----------------------------|  
|**Texto**|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|**Long**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|**Boolean**|Cyclical, Discrete, Ordered|  
|**Doble**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|**Date**|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  Los tipos de contenido Time y Sequence solo son compatibles con algoritmos de otros proveedores. Se admiten los tipos de contenido cíclicos y ordenados, pero la mayoría de los algoritmos los tratan como valores discretos y no realizan ningún procesamiento especial.  
  
 La tabla también muestra los *tipos de contenido* admitidos para cada tipo de datos.  
  
 El tipo de contenido es específico de la minería de datos y permite personalizar el modo en que se procesan o se calculan los datos en el modelo de minería. Por ejemplo, incluso aunque la columna contenga números, podría tener que modelarlos como valores discretos. Si la columna contiene números, también puede especificar que se discreticen o que el modelo los trate como valores continuos. Por lo tanto, el tipo de contenido puede tener una gran repercursión en el modelo. Para obtener una lista de todos los tipos de contenido, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
> [!NOTE]  
>  En otro sistemas de aprendizaje automático, podría encontrar los términos *datos nominales*, *factores* o *categorías*, *datos ordinales*o *datos de secuencia*. En general, se corresponden con los tipos de contenido. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el tipo de datos solo especifica el tipo de valor para el almacenamiento, no su uso en el modelo.  
  
## <a name="specifying-a-data-type"></a>Especificar un tipo de datos  
 Si crea el modelo de minería directamente con Extensiones de minería de datos (DMX), puede definir el tipo de datos de cada columna cuando defina el modelo y Analysis Services creará la estructura de minería correspondiente con los tipos de datos especificados al mismo tiempo. Si crea el modelo o la estructura de minería con un asistente, Analysis Services le sugerirá un tipo de datos o podrá elegir uno de una lista.  
  
## <a name="changing-a-data-type"></a>Cambiar un tipo de datos  
 Si cambia el tipo de datos de una columna, debe volver a procesar siempre la estructura de minería y todos los modelos de minería basados en esa estructura. En algunas ocasiones, al cambiar el tipo de datos la columna ya no se utilizará en el modelo en cuestión. En ese caso, Analysis Services producirá un error cuando se vuelva a procesar el modelo o procesará el modelo pero no incluirá esa columna en concreto.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Tipos de contenido &#40;DMX&#41;](../../dmx/content-types-dmx.md)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Tipos de datos &#40; DMX &#41;](../../dmx/data-types-dmx.md)   
 [Columnas del modelo de minería de datos](../../analysis-services/data-mining/mining-model-columns.md)   
 [Columnas de la estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
