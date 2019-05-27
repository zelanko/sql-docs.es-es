---
title: Distribuciones de columnas (minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- normal distribution type [data mining]
- uniform distribution type [data mining]
- columns [data mining], distributions
- log normal distribution type [data mining]
- continuous columns
- distributions [data mining]
ms.assetid: 87e700de-32be-4bc8-b01d-ba4ee1ab48de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5db71b5a94285f8ae63afeb65bec3f9807f8da27
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085705"
---
# <a name="column-distributions-data-mining"></a>Distribuciones de columnas (minería de datos)
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]puede definir distribuciones de columnas en una estructura de minería de datos para modificar la forma en que los algoritmos procesan los datos de estas columnas cuando se crean modelos de minería de datos. Para algunos algoritmos, resulta útil definir la distribución de las columnas continuas antes de procesar el modelo, si se sabe que las columnas contienen distribuciones de valores comunes. Si no define las distribuciones, los modelos de minería de datos resultantes podrían generar predicciones menos precisas que si se definieran las distribuciones porque los algoritmos disponen de menos información con la que interpretar los datos.  
  
 Los algoritmos que están disponibles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admiten los siguientes tipos de distribución:  
  
 `Normal`  
 Los valores de la columna continua forman un histograma con una distribución normal.  
  
 ![Histograma con distribución normal](../media/normal-distribution.gif "histograma con distribución normal")  
  
 `Log Normal`  
 Los valores de la columna continua forman un histograma, donde la curva se alarga en el extremo superior y se desvía hacia el extremo inferior.  
  
 ![Histograma con distribución log-normal](../media/log-normal-distribution.gif "histograma con distribución log-normal")  
  
 `Uniform`  
 Los valores de la columna continua forman una curva plana, en la que todos los valores tienen la misma probabilidad.  
  
 ![Histograma con distribución uniforme](../media/uniform-distribution.gif "histograma con distribución uniforme")  
  
 Para más información sobre los algoritmos que proporciona [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md)   
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-structures-analysis-services-data-mining.md)   
 [Métodos de discretización &#40;minería de datos&#41;](discretization-methods-data-mining.md)   
 [Distribuciones &#40;DMX&#41;](/sql/dmx/distributions-dmx)   
 [Columnas de la estructura de minería de datos](mining-structure-columns.md)  
  
  
