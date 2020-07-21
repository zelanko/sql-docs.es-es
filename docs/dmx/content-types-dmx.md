---
title: Tipos de contenido (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 30f5496247bb817d4ea7da08f95fe4a1b54dea5d
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669794"
---
# <a name="content-types-dmx"></a>Tipos de contenido (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Los algoritmos de minería de datos requieren información adicional además del tipo de datos para funcionar correctamente, como el tipo de contenido. El tipo de contenido ayuda al algoritmo a determinar la forma en que debe trabajar con los datos de la columna.  
  
 Cada algoritmo admite tipos de contenido específicos. Por ejemplo, el algoritmo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)] no puede usar columnas continuas. Para usar un columna continua en un modelo de Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)], debe discretizar los datos de la columna. Algunos algoritmos requieren determinados tipos de contenido para poder funcionar correctamente. Por ejemplo, el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] requiere una columna Key Time para identificar el período de tiempo durante el que se recopilaron los datos.  
  
 Para obtener una descripción completa de los tipos de contenido que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite, vea [tipos de contenido &#40;&#41;de minería de datos ](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining).  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
