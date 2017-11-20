---
title: Tipos (DMX) de contenido | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], content types
- content types [DMX]
- DMX [Analysis Services], content types
ms.assetid: ab9dd887-df8d-4878-96b0-635881892573
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 33af21a44066e96223bbfc07e39f4718edf87fc2
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="content-types-dmx"></a>Tipos de contenido (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Los algoritmos de minería de datos requieren información adicional además del tipo de datos para funcionar correctamente, como el tipo de contenido. El tipo de contenido ayuda al algoritmo a determinar la forma en que debe trabajar con los datos de la columna.  
  
 Cada algoritmo admite tipos de contenido específicos. Por ejemplo, el algoritmo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)] no puede usar columnas continuas. Para usar un columna continua en un modelo de Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)], debe discretizar los datos de la columna. Algunos algoritmos requieren determinados tipos de contenido para poder funcionar correctamente. Por ejemplo, el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] requiere una columna Key Time para identificar el período de tiempo durante el que se recopilaron los datos.  
  
 Para obtener una descripción completa del contenido tipos que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite, consulte [tipos de contenido &#40; minería de datos &#41;](../analysis-services/data-mining/content-types-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40; Analysis Services: minería de datos &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

