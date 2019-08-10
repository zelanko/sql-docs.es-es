---
title: Uso (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b961282ba6bc25caa260a3e156f843a413a5ef1a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893112"
---
# <a name="usage-dmx"></a>Uso (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Al utilizar extensiones de minería de datos (DMX) para definir un nuevo modelo de minería [!INCLUDE[msCoName](../includes/msconame-md.md)] de datos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], debe especificar cómo usará cada columna el algoritmo de minería de datos que genera el modelo. Puede especificar los siguientes tipos para una columna:  
  
-   **Key**  
  
-   **Secuencia de claves**  
  
-   **Hora clave**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 Las columnas cuyo tipo no se especifique en DMX se tratan como columnas de entrada.  
  
 Para procesar correctamente un modelo, el algoritmo debe conocer la columna de clave que identifica cada fila de manera única, la columna de destino para crear predicciones si se va a crear un modelo de predicción y las columnas que deben usarse como columnas de entrada para crear las relaciones que predicen la columna de destino.  
  
 Las columnas que se especifican como el tipo de predicción se usan como columnas de entrada y de salida. Las columnas que se especifican como **PredictOnly** solo se usan como columnas de salida. Algunos algoritmos pueden tratar las columnas Predict de forma distinta.  
  
 Para obtener más información sobre los tipos de uso [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de columnas que admite, vea [columnas del modelo de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
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
  
  
