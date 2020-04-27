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
ms.openlocfilehash: 6c7eab32f251b9622c6ac77febf2c004806c024b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174653"
---
# <a name="column-distributions-data-mining"></a>Distribuciones de columnas (minería de datos)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede definir distribuciones de columnas en una estructura de minería de datos, para que los algoritmos puedan procesar los datos de esas columnas cuando se crean modelos de minería de datos. Para algunos algoritmos, resulta útil definir la distribución de las columnas continuas antes de procesar el modelo, si se sabe que las columnas contienen distribuciones de valores comunes. Si no define las distribuciones, los modelos de minería de datos resultantes podrían generar predicciones menos precisas que si se definieran las distribuciones porque los algoritmos disponen de menos información con la que interpretar los datos.

 Los algoritmos que están disponibles en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admiten los siguientes tipos de distribución:

 `Normal`Los valores de la columna continua forman un histograma con una distribución normal.

 ![Histograma con distribución normal](../media/normal-distribution.gif "Histograma con distribución normal")

 `Log Normal`Los valores de la columna continua forman un histograma, donde la curva se alarga en el extremo superior y se sesga hacia el extremo inferior.

 ![Histograma con distribución normal del registro](../media/log-normal-distribution.gif "Histograma con distribución normal del registro")

 `Uniform`Los valores de la columna continua forman una curva plana, en la que todos los valores son igualmente probables.

 ![Histograma con distribución uniforme](../media/uniform-distribution.gif "Histograma con distribución uniforme")

 Para más información sobre los algoritmos que proporciona [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vea [Algoritmos de minería de datos &#40;Analysis Services - Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md).

## <a name="see-also"></a>Consulte también
 [Tipos de contenido &#40;](content-types-data-mining.md) [estructuras de minería de datos&#41;de minería de datos &#40;Analysis Services-minería de datos&#41;métodos de](mining-structures-analysis-services-data-mining.md) [discretización &#40;](discretization-methods-data-mining.md) [distribuciones](/sql/dmx/distributions-dmx)&#41;de minería de datos &#40;DMX&#41;columnas de la [estructura de minería](mining-structure-columns.md) de datos


