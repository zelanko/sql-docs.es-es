---
title: "Distribuciones de columnas (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 96b2502e351f371163d5b748b432d381d237a8a9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="column-distributions-data-mining"></a>Distribuciones de columnas (minería de datos)
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]puede definir distribuciones de columnas en una estructura de minería de datos para modificar la forma en que los algoritmos procesan los datos de estas columnas cuando se crean modelos de minería de datos. Para algunos algoritmos, resulta útil definir la distribución de las columnas continuas antes de procesar el modelo, si se sabe que las columnas contienen distribuciones de valores comunes. Si no define las distribuciones, los modelos de minería de datos resultantes podrían generar predicciones menos precisas que si se definieran las distribuciones porque los algoritmos disponen de menos información con la que interpretar los datos.  
  
 Los algoritmos que están disponibles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admiten los siguientes tipos de distribución:  
  
 **Normal**  
 Los valores de la columna continua forman un histograma con una distribución normal.  
  
 ![Histograma con distribución normal](../../analysis-services/data-mining/media/normal-distribution.gif "histograma con distribución normal")  
  
 **Logarítmica normal**  
 Los valores de la columna continua forman un histograma, donde la curva se alarga en el extremo superior y se desvía hacia el extremo inferior.  
  
 ![Histograma con distribución normal del registro](../../analysis-services/data-mining/media/log-normal-distribution.gif "histograma con distribución normal del registro")  
  
 **Uniforme**  
 Los valores de la columna continua forman una curva plana, en la que todos los valores tienen la misma probabilidad.  
  
 ![Histograma con distribución uniforme](../../analysis-services/data-mining/media/uniform-distribution.gif "histograma con distribución uniforme")  
  
 Para más información sobre los algoritmos que proporciona [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Métodos de discretización &#40; minería de datos &#41;](../../analysis-services/data-mining/discretization-methods-data-mining.md)   
 [Distribuciones &#40; DMX &#41;](../../dmx/distributions-dmx.md)   
 [Columnas de la estructura de minería de datos](../../analysis-services/data-mining/mining-structure-columns.md)  
  
  
