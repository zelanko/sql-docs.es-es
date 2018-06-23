---
title: Distribuciones de columnas (minería de datos) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
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
manager: mblythe
ms.openlocfilehash: 5170f490f6e6940b2d5bf4d8f7de7880f88d2e7e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103932"
---
# <a name="column-distributions-data-mining"></a>Distribuciones de columnas (minería de datos)
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]puede definir distribuciones de columnas en una estructura de minería de datos para modificar la forma en que los algoritmos procesan los datos de estas columnas cuando se crean modelos de minería de datos. Para algunos algoritmos, resulta útil definir la distribución de las columnas continuas antes de procesar el modelo, si se sabe que las columnas contienen distribuciones de valores comunes. Si no define las distribuciones, los modelos de minería de datos resultantes podrían generar predicciones menos precisas que si se definieran las distribuciones porque los algoritmos disponen de menos información con la que interpretar los datos.  
  
 Los algoritmos que están disponibles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admiten los siguientes tipos de distribución:  
  
 `Normal`  
 Los valores de la columna continua forman un histograma con una distribución normal.  
  
 ![Histograma con distribución normal](../media/normal-distribution.gif "histograma con distribución normal")  
  
 `Log Normal`  
 Los valores de la columna continua forman un histograma, donde la curva se alarga en el extremo superior y se desvía hacia el extremo inferior.  
  
 ![Histograma con distribución normal del registro](../media/log-normal-distribution.gif "histograma con distribución normal del registro")  
  
 `Uniform`  
 Los valores de la columna continua forman una curva plana, en la que todos los valores tienen la misma probabilidad.  
  
 ![Histograma con distribución uniforme](../media/uniform-distribution.gif "histograma con distribución uniforme")  
  
 Para más información sobre los algoritmos que proporciona [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services: minería de datos&#41;](mining-structures-analysis-services-data-mining.md)   
 [Métodos de discretización &#40;minería de datos&#41;](discretization-methods-data-mining.md)   
 [Distribuciones &#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [Columnas de la estructura de minería de datos](mining-structure-columns.md)  
  
  
