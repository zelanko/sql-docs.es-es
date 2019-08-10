---
title: Tipos de contenido (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: da8a5e5602b877c12284d8410f6b2a1c7da6bc58
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68889142"
---
# <a name="content-types-dmx"></a>Tipos de contenido (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Los algoritmos de minería de datos requieren información adicional además del tipo de datos para funcionar correctamente, como el tipo de contenido. El tipo de contenido ayuda al algoritmo a determinar la forma en que debe trabajar con los datos de la columna.  
  
 Cada algoritmo admite tipos de contenido específicos. Por ejemplo, el algoritmo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)] no puede usar columnas continuas. Para usar un columna continua en un modelo de Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)], debe discretizar los datos de la columna. Algunos algoritmos requieren determinados tipos de contenido para poder funcionar correctamente. Por ejemplo, el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] requiere una columna Key Time para identificar el período de tiempo durante el que se recopilaron los datos.  
  
 Para obtener una descripción completa de los tipos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] contenido que admite, vea [tipos &#40;de&#41;contenido minería de datos](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementos de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referencia de funciones &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia del operador &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de la &#40;instrucción&#41; DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones &#40;de predicción generales DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
