---
title: Contenido del modelo para los modelos de regresión lineal de minería de datos (Analysis Services - minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- mining model content, linear regression models
- regression algorithms [Analysis Services]
ms.assetid: a6abcb75-524e-4e0a-a375-c10475ac0a9d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 933b56aaa6e364ce55cac8832fc577acc061d510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66083643"
---
# <a name="mining-model-content-for-linear-regression-models-analysis-services---data-mining"></a>Contenido del modelo de minería de datos para los modelos de regresión lineal (Analysis Services - Minería de datos)
  En este tema se describe el contenido del modelo de minería de datos específico de los modelos que utilizan el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obtener una explicación general sobre el contenido del modelo de minería de datos para todos los tipos de modelo, vea [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md).  
  
## <a name="understanding-the-structure-of-a-linear-regression-model"></a>Descripción de la estructura de un modelo de regresión lineal  
 Un modelo de regresión lineal tiene una estructura sumamente simple. Cada modelo tiene un único nodo primario que representa el modelo y sus metadatos y un nodo de árbol de regresión (NODE_TYPE = 25) que contiene la fórmula de regresión para cada atributo de predicción.  
  
 ![Estructura del modelo de regresión lineal de](../media/modelcontentstructure-linreg.gif "estructura del modelo de regresión lineal")  
  
 Los modelos de regresión lineal usan el mismo algoritmo que los árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , pero se utilizan parámetros diferentes para restringir el árbol y solo se aceptan como entradas los atributos continuos. Sin embargo, dado que los modelos de regresión lineal se basan en el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , los modelos de regresión lineal se muestran utilizando el Visor de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para más información, vea [Examinar un modelo usando el Visor de árboles de Microsoft](browse-a-model-using-the-microsoft-tree-viewer.md).  
  
 En la sección siguiente se explica cómo interpretar la información del nodo de la fórmula de regresión. Esta información se aplica no solo a los modelos de regresión lineal, sino también a los modelos de árboles de decisión que contienen regresiones en una parte del árbol.  
  
## <a name="model-content-for-a-linear-regression-model"></a>Contenido de un modelo de regresión lineal  
 En esta sección solo se proporcionan detalles y ejemplos de las columnas del contenido del modelo de minería de datos que tienen una relevancia especial para la regresión lineal.  
  
 Para más información sobre las columnas de uso general en el conjunto de filas de esquema, vea [Mining Model Content &#40;Analysis Services - Data Mining&#41;](mining-model-content-analysis-services-data-mining.md).  
  
 MODEL_CATALOG  
 Nombre de la base de datos en la que se almacena el modelo.  
  
 MODEL_NAME  
 Nombre del modelo.  
  
 ATTRIBUTE_NAME  
 **Nodo raíz:** En blanco  
  
 **Nodo de regresión:** El nombre del atributo predecible.  
  
 NODE_NAME  
 Siempre lo mismo que NODE_UNIQUE_NAME.  
  
 NODE_UNIQUE_NAME  
 Identificador único para el nodo dentro del modelo. Este valor no puede modificarse.  
  
 NODE_TYPE  
 Un modelo de regresión lineal genera los tipos de nodos siguientes:  
  
|Identificador del tipo de nodo|Tipo|Descripción|  
|------------------|----------|-----------------|  
|25|Raíz del árbol de regresión|Contiene la fórmula que describe la relación entre la variable de entrada y la de salida.|  
  
 NODE_CAPTION  
 Etiqueta o título asociado al nodo. Esta propiedad se usa principalmente para la presentación.  
  
 **Nodo raíz:** En blanco  
  
 **Nodo de regresión:** Todos.  
  
 CHILDREN_CARDINALITY  
 Cálculo del número de elementos secundarios que tiene el nodo.  
  
 **Nodo raíz:** Indica el número de nodos de regresión. Se crea un nodo de regresión para cada atributo de predicción del modelo.  
  
 **Nodo de regresión:** Siempre es 0.  
  
 PARENT_UNIQUE_NAME  
 Nombre único del nodo primario del nodo. Se devuelve NULL para todos los nodos del nivel raíz.  
  
 NODE_DESCRIPTION  
 Descripción del nodo.  
  
 **Nodo raíz:** En blanco  
  
 **Nodo de regresión:** Todos.  
  
 NODE_RULE  
 No se utiliza para los modelos de regresión lineal.  
  
 MARGINAL_RULE  
 No se utiliza para los modelos de regresión lineal.  
  
 NODE_PROBABILITY  
 Probabilidad asociada a este nodo.  
  
 **Nodo raíz:** 0  
  
 **Nodo de regresión:** 1  
  
 MARGINAL_PROBABILITY  
 Probabilidad de alcanzar el nodo desde el nodo primario.  
  
 **Nodo raíz:** 0  
  
 **Nodo de regresión:** 1  
  
 NODE_DISTRIBUTION  
 Tabla anidada que proporciona estadísticas sobre los valores del nodo.  
  
 **Nodo raíz:** 0  
  
 **Nodo de regresión:** Una tabla que contiene los elementos utilizados para generar la fórmula de regresión. Un nodo de regresión contiene los tipos de valores siguientes:  
  
|VALUETYPE|  
|---------------|  
|1 (ausente)|  
|3 (continuo)|  
|7 (coeficiente)|  
|8 (ganancia de puntuación)|  
|9 (estadísticas)|  
|11 (intersección)|  
  
 NODE_SUPPORT  
 Número de casos que admiten este nodo.  
  
 **Nodo raíz:** 0  
  
 **Nodo de regresión:** Recuento de casos de entrenamiento.  
  
 MSOLAP_MODEL_COLUMN  
 Nombre del atributo de predicción.  
  
 MSOLAP_NODE_SCORE  
 Igual que NODE_PROBABILITY  
  
 MSOLAP_NODE_SHORT_CAPTION  
 Etiqueta que se utiliza para la visualización.  
  
## <a name="remarks"></a>Comentarios  
 Al crear un modelo utilizando el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , el motor de minería de datos crea una instancia especial de un modelo de árboles de decisión y proporciona los parámetros que restringen el árbol para contener todos los datos de entrenamiento en un único nodo. Todas las entradas continuas se marcan y evalúan como regresores potenciales, pero únicamente los que se ajusten a los datos se conservan como regresores en el modelo final. El análisis genera una única fórmula de regresión o ninguna fórmula para cada regresor.  
  
 Para ver la fórmula de regresión completa en la **Leyenda de minería de datos**, haga clic en el nodo **(Todos)** del [Visor de árboles de Microsoft](browse-a-model-using-the-microsoft-tree-viewer.md).  
  
 Además, al crear un modelo de árboles de decisión que incluye un atributo de predicción continuo, a veces el árbol tiene nodos de regresión que comparten las propiedades de los nodos del árbol de regresión.  
  
##  <a name="NodeDist_Regression"></a> Distribución de nodos para los atributos continuos  
 La mayoría de la información importante en un nodo de regresión está incluida en la tabla NODE_DISTRIBUTION. En el ejemplo siguiente se muestra el diseño de la tabla NODE_DISTRIBUTION. En este ejemplo, la estructura de minería de datos de Targeted Mailing se ha utilizado para crear un modelo de regresión lineal que predice los ingresos de los clientes según su edad. La finalidad del modelo es únicamente ilustrativo, porque puede generarse con facilidad utilizando los datos y la estructura de minería de datos de ejemplo existentes de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|Support|PROBABILITY|VARIANCE|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|1|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Age|471.687717702463|0|0|126.969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 La tabla NODE_DISTRIBUTION contiene varias filas, cada una agrupada por una variable. Las primeras dos filas siempre son de los tipos de valores 1 y 3, y describen el atributo de destino. Las filas siguientes proporcionan los detalles sobre la fórmula para un *regresor*determinado. Un regresor es una variable de entrada que tiene una relación lineal con la variable de salida. Puede haber varios regresores y cada uno tendrá una fila independiente para el coeficiente (VALUETYPE = 7), la ganancia de puntuación (VALUETYPE = 8) y las estadísticas (VALUETYPE = 9). Finalmente, la tabla incluye una fila que contiene la intersección de la ecuación (VALUETYPE = 11).  
  
### <a name="elements-of-the-regression-formula"></a>Elementos de la fórmula de regresión  
 La tabla NODE_DISTRIBUTION anidada contiene cada elemento de la fórmula de regresión en una fila independiente. Las dos primeras filas de datos en los resultados del ejemplo contienen información sobre el atributo de predicción, **Yearly Income**, que modela la variable dependiente. La columna SUPPORT muestra el recuento de casos de compatibilidad de los dos estados de este atributo: o bien hay disponible un valor **Yearly Income** o el valor **Yearly Income** no está.  
  
 La columna VARIANCE indica la varianza calculada del atributo de predicción. La*varianza* es una medida de la dispersión de los valores de un ejemplo, dada una distribución esperada. La varianza aquí se calcula tomando el promedio de la desviación cuadrada de la media. La raíz cuadrada de la varianza también se conoce como desviación estándar. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no proporciona la desviación estándar pero se puede calcular fácilmente.  
  
 Para cada regresor se generan tres filas. Contienen el coeficiente, la ganancia de puntuación y estadísticas de regresores.  
  
 Finalmente, la tabla contiene una fila que proporciona la intersección de la ecuación.  
  
#### <a name="coefficient"></a>Coeficiente  
 Para cada regresor se calcula un coeficiente (VALUETYPE = 7). El propio coeficiente aparece en la columna ATTRIBUTE_VALUE, mientras que la columna VARIANCE indica la varianza para el coeficiente. Los coeficientes se calculan con una linealidad máxima.  
  
#### <a name="score-gain"></a>Ganancia de puntuación  
 La ganancia de puntuación (VALUETYPE = 8) de cada regresor representa la puntuación de grado de interés del atributo. Puede utilizar este valor para calcular la utilidad de varios regresores.  
  
#### <a name="statistics"></a>Estadísticas  
 La estadística de regresores (VALUETYPE = 9) es la media del atributo para los casos que tienen un valor. La columna ATTRIBUTE_VALUE contiene la propia media, mientras que la columna VARIANCE contiene la suma de desviaciones de la media.  
  
#### <a name="intercept"></a>Interceptar  
 Normalmente, la *intersección* (VALUETYPE = 11) o *valor residual* en una ecuación de regresión indica el valor del atributo de predicción en el punto donde el atributo de entrada es igual a 0. En muchos casos, esto podría no suceder y se podrían producir resultados poco intuitivos.  
  
 Por ejemplo, en un modelo que prediga los ingresos según la edad, es inútil obtener información sobre los ingresos a los 0 años. En la vida real, suele ser más útil saber el comportamiento en el margen con respecto a los valores medios. Por consiguiente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modifica la intersección para expresar cada regresor en una relación con la media.  
  
 Este ajuste es difícil de ver en el contenido del modelo de minería de datos, pero es obvio si se ve la ecuación completada en la **Leyenda de minería de datos** del **Visor de árboles de Microsoft**. La fórmula de regresión se desvía del punto 0 al punto que representa la media. Esto presenta una vista que es más intuitiva dados los datos actuales.  
  
 Por consiguiente, suponiendo que la edad media está alrededor de 45 años, la intersección (VALUETYPE = 11) para la fórmula de regresión indica los ingresos medios.  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](mining-model-content-analysis-services-data-mining.md)   
 [Algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm.md)   
 [Referencia técnica del algoritmo de regresión lineal de Microsoft](microsoft-linear-regression-algorithm-technical-reference.md)   
 [Ejemplos de consultas de modelos de regresión lineal](linear-regression-model-query-examples.md)  
  
  
