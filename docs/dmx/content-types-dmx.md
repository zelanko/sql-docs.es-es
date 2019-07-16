---
title: (DMX) de tipos de contenido | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ec3b618e83fff2915ec7d1dac0f25ea82c60912c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071025"
---
# <a name="content-types-dmx"></a>Tipos de contenido (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Los algoritmos de minería de datos requieren información adicional además del tipo de datos para funcionar correctamente, como el tipo de contenido. El tipo de contenido ayuda al algoritmo a determinar la forma en que debe trabajar con los datos de la columna.  
  
 Cada algoritmo admite tipos de contenido específicos. Por ejemplo, el algoritmo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)] no puede usar columnas continuas. Para usar un columna continua en un modelo de Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)], debe discretizar los datos de la columna. Algunos algoritmos requieren determinados tipos de contenido para poder funcionar correctamente. Por ejemplo, el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] requiere una columna Key Time para identificar el período de tiempo durante el que se recopilaron los datos.  
  
 Para obtener una descripción completa del contenido de tipos que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite, consulte [tipos de contenido &#40;minería de datos&#41;](../analysis-services/data-mining/content-types-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
