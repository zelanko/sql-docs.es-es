---
title: Referencia técnica del algoritmo Bayes Naive de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MINIMUM_DEPENDENCY_PROBABILITY parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
ms.assetid: a4cd47fe-2127-4930-b18f-3edd17ee9a65
caps.latest.revision: 16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e0f489c08c33fa66794f0eace23d207855e207b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253537"
---
# <a name="microsoft-naive-bayes-algorithm-technical-reference"></a>Referencia técnica del algoritmo Bayes naive de Microsoft
  El algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo de clasificación que proporciona [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para el modelado predictivo. Este algoritmo calcula la probabilidad condicional entre columnas de entrada y de predicción y supone que las columnas son independientes. Esta suposición de independencia conduce al nombre Bayes naive.  
  
## <a name="implementation-of-the-microsoft-naive-bayes-algorithm"></a>Implementación del algoritmo Bayes naive de Microsoft  
 Desde el punto de vista computacional, el algoritmo es menos complejo que otros algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] y, por tanto, resulta útil para generar rápidamente modelos de minería de datos que detectan las relaciones entre las columnas de entrada y las columnas de predicción. El algoritmo considera cada par de valores de atributos de entrada y de atributos de salida.  
  
 La descripción de las propiedades matemáticas del Teorema de Bayes queda fuera del ámbito de esta documentación; para obtener más información, vea el documento de Microsoft Research titulado [Redes bayesianas: la combinación de conocimiento y datos estadísticos](http://go.microsoft.com/fwlink/?LinkId=207029).  
  
 Para obtener la descripción de cómo se ajustan las probabilidades en todos los modelos para tener en cuenta los valores ausentes posibles, vea [Valores ausentes &#40;Analysis Services - Minería de datos&#41;](missing-values-analysis-services-data-mining.md).  
  
### <a name="feature-selection"></a>Selección de características  
 El algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] realiza la selección automática de las características para limitar el número de valores que se consideran al generar el modelo. Para obtener más información, vea [Selección de características &#40;minería de datos&#41;](feature-selection-data-mining.md).  
  
|Algoritmo|Método de análisis|Comentarios|  
|---------------|------------------------|--------------|  
|Bayes naive|Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|Bayes naive solo acepta atributos discretos o de datos discretos, por lo que no puede utilizar la puntuación de grado de interés.|  
  
 El algoritmo está diseñado para reducir al mínimo el tiempo de proceso y seleccionar eficazmente los atributos que tienen la importancia máxima; sin embargo, puede controlar los datos que el algoritmo utiliza estableciendo los parámetros como se indica a continuación:  
  
-   Para limitar los valores que se utilizan como entradas, disminuya el valor de MAXIMUM_INPUT_ATTRIBUTES.  
  
-   Para limitar el número de atributos analizados por el modelo, disminuya el valor de MAXIMUM_OUTPUT_ATTRIBUTES.  
  
-   Para limitar el número de valores que pueden considerarse para cualquier un atributo, disminuya el valor de MINIMUM_STATES.  
  
## <a name="customizing-the-naive-bayes-algorithm"></a>Personalizar el algoritmo Bayes naive  
 El algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite varios parámetros que influyen en el comportamiento, el rendimiento y la precisión del modelo de minería de datos resultante. También puede establecer marcas de modelado en las columnas de modelo para controlar cómo se procesan los datos, o establecer marcas en la estructura de minería de datos para especificar cómo se deberían administrar los valores nulos o que faltan.  
  
### <a name="setting-algorithm-parameters"></a>Establecer parámetros del algoritmo  
 El algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite varios parámetros que influyen en el rendimiento y la precisión del modelo de minería de datos resultante. Estos parámetros se describen en la tabla siguiente.  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Especifica el número máximo de atributos de entrada que el algoritmo puede procesar antes de invocar la selección de características. La función de selección de atributos de entrada se deshabilita cuando este valor se establece en 0.  
  
 El valor predeterminado es 255.  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Especifica el número máximo de atributos de salida que puede administrar el algoritmo antes de invocar la selección de características. La característica de selección de atributos de salida se deshabilita cuando este valor se establece en 0.  
  
 El valor predeterminado es 255.  
  
 *MINIMUM_DEPENDENCY_PROBABILITY*  
 Especifica la probabilidad de dependencia mínima entre los atributos de entrada y salida. Este valor se utiliza para limitar el tamaño del contenido generado por el algoritmo. El valor de esta propiedad puede establecerse en un valor comprendido entre 0 y 1. Los valores mayores reducen el número de atributos en el contenido del modelo.  
  
 El valor predeterminado es 0,5.  
  
 *MAXIMUM_STATES*  
 Especifica el número máximo de estados de atributo que admite el algoritmo. Si el número de estados que tiene un atributo es mayor que el número máximo de estados, el algoritmo utiliza los estados más conocidos del atributo e interpreta que faltan los estados restantes.  
  
 El valor predeterminado es 100.  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las marcas de modelado siguientes. Al crear la estructura o el modelo de minería de datos, se definen las marcas de modelado que especifican cómo se tratan los valores de cada columna durante el análisis. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](modeling-flags-data-mining.md).  
  
|Marca de modelado|Descripción|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Significa que la columna se tratará como si tuviera dos estados posibles: ausente y existente. Un valor NULL es un valor ausente.<br /><br /> Se aplica a la columna del modelo de minería de datos.|  
|NOT NULL|Indica que la columna no puede contener un valor NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.<br /><br /> Se aplica a la columna de la estructura de minería de datos.|  
  
## <a name="requirements"></a>Requisitos  
 Un modelo de árbol de Bayes naive debe contener una columna de clave, al menos un atributo de predicción y al menos un atributo de entrada. Ningún atributo puede ser continuo; si los datos contienen datos numéricos continuos, se omitirán o se convertirán en discretos.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo Bayes naive de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se enumeran en la tabla siguiente. Para más información sobre el significado de los tipos de contenido usados en un modelo de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md).  
  
|columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Cíclico, discreto, discretizado, clave, tabla y ordenado|  
|Atributo de predicción|Cíclico, discreto, discretizado, tabla y ordenado|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido Cyclical y Ordered, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo Bayes Naive de Microsoft](microsoft-naive-bayes-algorithm.md)   
 [Ejemplos de consultas del modelo Bayes naive](naive-bayes-model-query-examples.md)   
 [Para los modelos Bayes Naive contenido del modelo de minería de datos &#40;Analysis Services - minería de datos&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
