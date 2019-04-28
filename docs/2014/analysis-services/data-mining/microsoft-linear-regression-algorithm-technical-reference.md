---
title: Referencia técnica del algoritmo de regresión lineal de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AUTO_DETECT_PERIODICITY parameter
- linear regression algorithms [Analysis Services]
- regression algorithms [Analysis Services]
ms.assetid: 7807b5ff-8e0d-418d-a05b-b1a9644536d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3a4bd34c0ce6a84ca4f9050f4c4b428123c379dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721907"
---
# <a name="microsoft-linear-regression-algorithm-technical-reference"></a>Referencia técnica del algoritmo de regresión lineal de Microsoft
  El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es una versión especial del algoritmo de árboles de decisión de Microsoft que está optimizado para modelar pares de atributos continuos. Este tema explica la implementación del algoritmo, describe cómo personalizar su comportamiento y proporciona vínculos a información adicional sobre cómo consultar los modelos.  
  
## <a name="implementation-of-the-linear-regression-algorithm"></a>Implementación del algoritmo de regresión lineal  
 El algoritmo de árboles de decisión de Microsoft se puede utilizar para muchas tareas: regresión lineal, clasificación o análisis de la asociación. Para implementar este algoritmo con el propósito de la regresión lineal, los parámetros del algoritmo se controlan para restringir el crecimiento del árbol y mantener todos los datos en el modelo en un nodo único. En otras palabras, aunque la regresión lineal está basada en un árbol de decisión, el árbol únicamente contiene una raíz y ninguna bifurcación: todos los datos residen en el nodo raíz.  
  
 Para lograr esto, el parámetro *MINIMUM_LEAF_CASES* del algoritmo se establece para ser mayor o igual que el número total de casos que el algoritmo usa para entrenar el modelo de minería de datos. Con el parámetro así establecido, el algoritmo no crea nunca una división y, por tanto, lleva a cabo una regresión lineal.  
  
 La ecuación que representa la recta de regresión toma la forma general de y = ax + b y se conoce como ecuación de regresión. La variable Y representa la variable de salida, X representa la variable de entrada, y a y b son coeficientes ajustables. Puede recuperar los coeficientes, intersecciones y otra información sobre la fórmula de regresión consultando el modelo de minería de datos completado. Para obtener más información, vea [Ejemplos de consultas de modelos de regresión lineal](linear-regression-model-query-examples.md).  
  
### <a name="scoring-methods-and-feature-selection"></a>Métodos de puntuación y selección de características  
 Todos los algoritmos de minería de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizan automáticamente la selección de características para mejorar el análisis y reducir la carga de procesamiento. El método utilizado para la selección de características en la regresión lineal es la puntuación de grado de interés, porque el modelo únicamente admite las columnas continuas. Como referencia, la tabla siguiente muestra la diferencia en la selección de características para el algoritmo de regresión lineal y el algoritmo de árboles de decisión.  
  
|Algoritmo|Método de análisis|Comentarios|  
|---------------|------------------------|--------------|  
|Regresión lineal|Puntuación interestingness|Predeterminado:<br /><br /> Otros métodos de selección de características que están disponibles con el algoritmo de árboles de decisión se aplican únicamente a las variables discretas y, por consiguiente, no son aplicables a los modelos de regresión lineal.|  
|Árboles de decisión|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|Si alguna columna contiene valores continuos no binarios, se utiliza la puntuación interestingness (grado de interés) en todas las columnas para asegurar la coherencia. En caso contrario, se utiliza el método predeterminado o el especificado.|  
  
 Los parámetros del algoritmo que controlan la selección de características para el modelo de árboles de decisión son MAXIMUM_INPUT_ATTRIBUTES y MAXIMUM_OUTPUT.  
  
## <a name="customizing-the-linear-regression-algorithm"></a>Personalizar el algoritmo de regresión lineal  
 El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite los parámetros que afectan al comportamiento, el rendimiento y la precisión del modelo de minería de datos resultante. También puede establecer marcas de modelado en las columnas del modelo de minería de datos o de la estructura de minería de datos para controlar la manera en que se procesan los datos.  
  
### <a name="setting-algorithm-parameters"></a>Establecer los parámetros del algoritmo  
 En la tabla siguiente se enumeran los parámetros que se proporcionan para el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*MAXIMUM_INPUT_ATTRIBUTES*|Define el número de atributos de entrada que el algoritmo puede controlar antes de invocar la selección de características. Establezca este valor en 0 para desactivar la selección de características.<br /><br /> El valor predeterminado es 255.|  
|*MAXIMUM_OUTPUT_ATTRIBUTES*|Define el número de atributos de salida que el algoritmo puede controlar antes de invocar la selección de características. Establezca este valor en 0 para desactivar la selección de características.<br /><br /> El valor predeterminado es 255.|  
|*FORCE_REGRESSOR*|Fuerza al algoritmo a usar las columnas indicadas como regresores, independientemente de su importancia según los cálculos del algoritmo.|  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las marcas de modelado siguientes. Al crear la estructura o el modelo de minería de datos, se definen las marcas de modelado que especifican cómo se tratan los valores de cada columna durante el análisis. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](modeling-flags-data-mining.md).  
  
|Marca de modelado|Descripción|  
|-------------------|-----------------|  
|NOT NULL|Indica que la columna no puede contener un valor NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.<br /><br /> Se aplica a las columnas de la estructura de minería de datos.|  
|REGRESSOR|Indica que la columna contiene valores numéricos continuos que se deberían tratar como posibles variables independientes durante el análisis.<br /><br /> Nota: Al marcar una columna como regresor no garantiza que la columna se utilizará como regresor en el modelo final.<br /><br /> Se aplica a las columnas del modelo de minería de datos.|  
  
### <a name="regressors-in-linear-regression-models"></a>Regresores en modelos de regresión lineal  
 Los modelos de regresión lineal se basan en el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Sin embargo, aun cuando no utilice el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , cualquier modelo de árbol de decisión puede contener un árbol o nodos que representen una regresión en un atributo continuo.  
  
 No es necesario especificar que una columna continua representa un regresor. El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] dividirá el conjunto de datos en regiones con patrones significativos aunque no establezca la marca REGRESSOR en la columna. La diferencia es que cuando se establece la marca de modelado, el algoritmo intentará buscar ecuaciones de regresión del formulario un * C1 + b\*C2 + … para ajustar los patrones en los nodos del árbol. Se calcula la suma de los valores residuales y, si la desviación es demasiado grande, se fuerza una división en el árbol.  
  
 Por ejemplo, si está prediciendo los hábitos de compra de los clientes utilizando **Income** como atributo y ha establecido la marca de modelado REGRESSOR en la columna, el algoritmo intentará en primer lugar ajustar los valores de **Income** mediante una fórmula de regresión estándar. Si la desviación es demasiado grande, se abandona la fórmula de regresión y el árbol se dividirá de acuerdo con algún otro atributo. A continuación, el algoritmo de árboles de decisión intentará ajustar un regresor para los ingresos en cada una de las ramas después de la división.  
  
 Puede utilizar el parámetro FORCED_REGRESSOR para garantizar que el algoritmo utilizará un regresor determinado. Este parámetro se puede utilizar con el algoritmo de árboles de decisión de Microsoft y el algoritmo de regresión lineal de Microsoft.  
  
## <a name="requirements"></a>Requisitos  
 Un modelo de regresión lineal debe contener una columna de clave, columnas de entrada y al menos una columna de predicción.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se incluyen en la tabla siguiente. Para más información sobre el significado de los tipos de contenido usados en un modelo de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](content-types-data-mining.md).  
  
|columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Continuo, cíclico, clave, tabla y ordenado|  
|Atributo de predicción|Continuo, cíclico y ordenado|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido `Cyclical` and `Ordered`, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm.md)   
 [Ejemplos de consultas de modelos de regresión lineal](linear-regression-model-query-examples.md)   
 [Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
