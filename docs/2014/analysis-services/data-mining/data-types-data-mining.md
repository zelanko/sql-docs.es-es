---
title: Tipos de datos (minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data types [data mining]
- columns [data mining], data types
- data mining [Analysis Services], data types
ms.assetid: 4af5b7db-790b-459c-b2b4-00f0cf6b5ce4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc810f56d552fa17cb027598a25bde114a696375
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084799"
---
# <a name="data-types-data-mining"></a>Tipos de datos (minería de datos)
  Cuando cree un modelo o una estructura de minería en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], deberá definir los tipos de datos de cada una de las columnas de la estructura. Los tipos de datos indican al motor de minería de datos si los datos del origen de datos son numéricos o de texto y cómo deben procesarse los datos. Por ejemplo, si el origen de datos contiene datos numéricos, puede especificar si los números deben tratarse como enteros o utilizando posiciones decimales.  
  
 Cada tipo de datos admite uno o varios tipos de contenido. Puede personalizar el modo en que se procesan o se calculan los datos de la columna en el modelo de minería estableciendo su tipo de contenido.  
  
 Por ejemplo, si tiene datos numéricos en una columna, puede elegir que se traten como tipos de datos numéricos o como texto. Si elige el tipo de datos numérico, puede establecer varios tipos de contenido diferentes: puede discretizar los números o tratarlos como valores continuos. Para obtener una lista de todos los tipos de contenido, vea [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite los tipos de datos siguientes para las columnas de estructura de minería:  
  
|Tipo de datos|Tipos de contenido admitidos|  
|---------------|-----------------------------|  
|`Text`|Cyclical, Discrete, Discretized, Key Sequence, Ordered, Sequence|  
|`Long`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|`Boolean`|Cyclical, Discrete, Ordered|  
|`Double`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered, Sequence, Time<br /><br /> Classified|  
|`Date`|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Key Time, Ordered|  
  
> [!NOTE]  
>  Los tipos de contenido Time y Sequence solo son compatibles con algoritmos de otros proveedores. Se admiten los tipos de contenido cíclicos y ordenados, pero la mayoría de los algoritmos los tratan como valores discretos y no realizan ningún procesamiento especial.  
  
## <a name="specifying-a-data-type"></a>Especificar un tipo de datos  
 Si crea el modelo de minería directamente con Extensiones de minería de datos (DMX), puede definir el tipo de datos de cada columna cuando defina el modelo y Analysis Services creará la estructura de minería correspondiente con los tipos de datos especificados al mismo tiempo. Si crea el modelo o la estructura de minería con un asistente, Analysis Services le sugerirá un tipo de datos o podrá elegir uno de una lista.  
  
## <a name="changing-a-data-type"></a>Cambiar un tipo de datos  
 Si cambia el tipo de datos de una columna, debe volver a procesar siempre la estructura de minería y todos los modelos de minería basados en esa estructura. En algunas ocasiones, al cambiar el tipo de datos la columna ya no se utilizará en el modelo en cuestión. En ese caso, Analysis Services producirá un error cuando se vuelva a procesar el modelo o procesará el modelo pero no incluirá esa columna en concreto.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md)   
 [Tipos de contenido &#40;DMX&#41;](/sql/dmx/content-types-dmx)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-structures-analysis-services-data-mining.md)   
 [Tipos de datos &#40;DMX&#41;](/sql/dmx/data-types-dmx)   
 [Columnas del modelo de minería de datos](mining-model-columns.md)   
 [Columnas de la estructura de minería de datos](mining-structure-columns.md)  
  
  
