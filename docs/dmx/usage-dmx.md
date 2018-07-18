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
manager: kfile
ms.openlocfilehash: 459d6a0240ac2588c0924eae7bdae348a71f5946
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37990989"
---
# <a name="usage-dmx"></a>Uso (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cuando usa las extensiones de minería de datos (DMX) para definir un nuevo modelo de minería de datos en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], debe especificar cómo el algoritmo de minería de datos que se basa el modelo usará cada columna. Puede especificar los siguientes tipos para una columna:  
  
-   **Key**  
  
-   **Secuencia de teclas**  
  
-   **Clave temporal**  
  
-   **Predict**  
  
-   **PredictOnly**  
  
 Las columnas cuyo tipo no se especifique en DMX se tratan como columnas de entrada.  
  
 Para procesar correctamente un modelo, el algoritmo debe conocer la columna de clave que identifica cada fila de manera única, la columna de destino para crear predicciones si se va a crear un modelo de predicción y las columnas que deben usarse como columnas de entrada para crear las relaciones que predicen la columna de destino.  
  
 Las columnas que se especifican como el **Predict** tipo se utilizan como columnas de entrada y salidas. Las columnas que se especifican como **PredictOnly** sólo se utilizan como columnas de salida. Algunos algoritmos pueden tratar las columnas Predict de forma distinta.  
  
 Para obtener más información acerca de la columna de tipos de uso que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite, consulte [columnas del modelo de minería de datos](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
