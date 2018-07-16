---
title: Objetos (Analysis Services - datos multidimensionales) de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d722b34679ccef20a939fc505e735886e7f16d1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282227"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Objetos de cubo (Analysis Services - Datos multidimensionales)
    
## <a name="introducing-cube-objects"></a>Introducción a los objetos de cubo  
 Un objeto <xref:Microsoft.AnalysisServices.Cube> simple se compone de la información básica, dimensiones y grupos de medida. La información básica incluye el nombre del cubo, la medida predeterminada del cubo, el origen de datos, el modo de almacenamiento y otros aspectos.  
  
 La colección Dimensions contiene el conjunto real de dimensiones que se utilizan en el cubo de la colección de dimensiones de la base de datos. Todas las dimensiones deben estar definidas en la colección de dimensiones de la base de datos para hacer referencia a ellas en el cubo. Las dimensiones privadas no están disponibles en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Los grupos de medida son conjuntos de medidas del cubo. Un grupo de medida es una colección de medidas con una vista del origen de datos común y un conjunto común de dimensiones. El grupo de medida es la unidad de proceso de las medidas; los grupos de medida se pueden procesar de forma individual y, a continuación, se pueden examinar.  
  
## <a name="in-this-section"></a>En esta sección  
  
|||  
|-|-|  
|Tema||  
|[Acciones &#40;Analysis Services - datos multidimensionales&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[Agregaciones y diseños de agregaciones](aggregations-and-aggregation-designs.md)||  
|[Cálculos](calculations.md)||  
|[Las celdas del cubo &#40;Analysis Services - datos multidimensionales&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[Propiedades del cubo](cube-properties-multidimensional-model-programming.md)||  
|[Almacenamiento de cubos &#40;Analysis Services - datos multidimensionales&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[Traducciones de cubo](cube-translations.md)||  
|[Relaciones de dimensión](dimension-relationships.md)||  
|[Indicadores de rendimiento clave &#40;KPI&#41; en modelos multidimensionales](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[Medidas y grupos de medida](../multidimensional-models/measures-and-measure-groups.md)||  
|[Las particiones &#40;Analysis Services - datos multidimensionales&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[Perspectivas](perspectives.md)||  
  
  
