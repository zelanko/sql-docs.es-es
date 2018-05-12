---
title: Referencia técnica del algoritmo de agrupación en clústeres de secuencia de Microsoft | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cf5f652cc2cec77fdbcb488710886441788a0631
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Referencia técnica del algoritmo de clústeres de secuencia de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El algoritmo de clústeres de secuencia de Microsoft es un algoritmo híbrido que usa el análisis de cadenas de Markov para identificar secuencias ordenadas, y combina los resultados de este análisis con técnicas de agrupación en clústeres para generar clústeres basados en las secuencias y otros atributos del modelo. En este tema se describe la implementación del algoritmo y cómo personalizarlo, y se detallan los requisitos especiales para los modelos de agrupación en clústeres de secuencia.  
  
 Para obtener más información general sobre el algoritmo, incluyendo cómo examinar y consultar los modelos de agrupación en clústeres de secuencia, vea [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md).  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Implementación del algoritmo de clústeres de secuencia de Microsoft  
 El modelo de agrupación en clústeres de secuencia de Microsoft usa modelos de Markov para identificar las secuencias y determinar su probabilidad. Un modelo de Markov es un gráfico dirigido que almacena las transiciones entre los diferentes estados. El algoritmo de clústeres de secuencia de Microsoft usa cadenas de Markov de orden n, no un modelo de Markov oculto.  
  
 El número de órdenes en una cadena de Markov indica cuántos estados se usan para determinar la probabilidad de los estados actuales. En un modelo de Markov de primer orden, la probabilidad del estado actual depende solo del estado anterior. En una cadena de Markov de segundo orden, la probabilidad de un estado depende de los dos estados previos, etc. En cada cadena de Markov, una matriz de transición almacena las transiciones para cada combinación de estados. A medida que aumenta la longitud de la cadena de Markov, el tamaño de la matriz aumenta también de forma exponencial y la matriz se vuelve sumamente dispersa. El tiempo de procesamiento también aumenta proporcionalmente.  
  
 Puede resultar útil visualizar la cadena usando el ejemplo del análisis clickstream, que analiza las visitas a las páginas web de un sitio. Cada usuario crea una larga secuencia de clics para cada sesión. Al crear un modelo para analizar el comportamiento del usuario en un sitio web, el conjunto de datos usado para el entrenamiento es una secuencia de direcciones URL, convertida en un gráfico que incluye el recuento de todas las instancias de la misma ruta de acceso de clics. Por ejemplo, el gráfico contiene la probabilidad de que el usuario se mueva de la página 1 a la página 2 (10%), la probabilidad de que el usuario se mueva de la página 1 a la página 3 (20%), etc. Al reunir todas las posibles rutas de acceso y partes de las rutas de acceso, se obtiene un gráfico que puede ser más largo y complejo que cualquier ruta de acceso única observada.  
  
 De forma predeterminada, el algoritmo de clústeres de secuencia de Microsoft usa el método de agrupación en clústeres Expectation Maximization (EM). Para obtener más información, vea [Referencia técnica del algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
 Los destinos de la agrupación en clústeres son los atributos secuenciales y los no secuenciales. Cada clúster se selecciona de forma aleatoria usando una distribución de probabilidad. Cada clúster tiene una cadena de Markov que representa el conjunto completo de rutas de acceso, y una matriz que contiene las transiciones de estado de secuencia y las probabilidades. En función de la distribución inicial, se usa la regla de Bayes para calcular la probabilidad de cualquier atributo, incluyendo una secuencia, en un clúster concreto.  
  
 El algoritmo de clústeres de secuencia de Microsoft admite la adición de atributos no secuenciales al modelo. Esto significa que los atributos adicionales se combinan con los atributos de secuencia para crear clústeres de casos con atributos similares, al igual que en un modelo de agrupación en clústeres típico.  
  
 Un modelo de agrupación en clústeres de secuencia tiende a crear muchos más clústeres que un modelo de agrupación en clústeres típico. Por lo tanto, el algoritmo de clústeres de secuencia de Microsoft realiza la *descomposición en clústeres*para separar clústeres en función de las secuencias y otros atributos.  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>Selección de características en un modelo de agrupación en clústeres de secuencia  
 La selección de características no se invoca al generar secuencias; sin embargo, la selección de características se aplica en la fase de agrupación en clústeres.  
  
|Tipo de modelo|Método de selección de características|Comentarios|  
|----------------|------------------------------|--------------|  
|Agrupación en clústeres de secuencia|No se utiliza|No se invoca la selección de características; sin embargo, se puede controlar el comportamiento del algoritmo estableciendo el valor de los parámetros MINIMUM_SUPPORT y MINIMUM_PROBABILITY.|  
|Agrupación en clústeres|Puntuación interestingness|Aunque el algoritmo de clústeres puede utilizar algoritmos discretos o de datos discretos, la puntuación de cada atributo se calcula como una distancia y es continua; por consiguiente, se utiliza la puntuación de grado de interés.|  
  
 Para más información, consulte [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
### <a name="optimizing-performance"></a>Optimizar el rendimiento  
 El algoritmo de clústeres de secuencia de Microsoft admite varias maneras de optimizar el procesamiento:  
  
-   Controlando el número de clústeres generados estableciendo un valor para el parámetro CLUSTER_COUNT.  
  
-   Reduciendo el número de secuencias incluidas como atributos incrementando el valor del parámetro MINIMUM_SUPPORT. Como resultado, se eliminan las secuencias raras.  
  
-   Reduciendo la complejidad antes de procesar el modelo mediante la agrupación de los atributos relacionados.  
  
 En general, puede optimizar el rendimiento de una cadena de Markov de orden n de varias maneras:  
  
-   Controlando la longitud de las posibles secuencias.  
  
-   Reduciendo mediante programación el valor de n.  
  
-   Almacenando solo las probabilidades que superan un umbral especificado.  
  
 Una discusión completa de estos métodos queda fuera del ámbito de este tema.  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>Personalizar el algoritmo de clústeres de secuencia de Microsoft  
 El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite parámetros que afectan al comportamiento, el rendimiento y la precisión del modelo de minería de datos resultante. También puede modificar el comportamiento del modelo completado estableciendo marcas de modelado que controlan la manera en que el algoritmo procesa los datos de entrenamiento.  
  
### <a name="setting-algorithm-parameters"></a>Establecer parámetros del algoritmo  
 En la tabla siguiente se describen los parámetros que se pueden utilizar con el algoritmo de clústeres de secuencia de Microsoft.  
  
 CLUSTER_COUNT  
 Especifica el número aproximado de clústeres que generará el algoritmo. Si no se puede generar el número aproximado de clústeres a partir de los datos, el algoritmo genera tantos clústeres como sea posible. Si el parámetro CLUSTER_COUNT se establece en 0, el algoritmo utiliza la heurística para determinar mejor el número de clústeres que va a generar.  
  
 El valor predeterminado es 10.  
  
> [!NOTE]  
>  La especificación de un número distinto de cero actúa como una sugerencia para el algoritmo, que continúa con el objetivo de encontrar el número especificado, pero puede encontrar más o menos.  
  
 MINIMUM_SUPPORT  
 Especifica el número mínimo de casos compatibles con un atributo necesarios para que se cree un clúster.  
  
 El valor predeterminado es 10.  
  
 MAXIMUM_SEQUENCE_STATES  
 Especifica el número máximo de estados que puede tener una secuencia.  
  
 Si se establece este valor en un número mayor que 100, el algoritmo puede crear un modelo que no proporcione información significativa.  
  
 El valor predeterminado es 64.  
  
 MAXIMUM_STATES  
 Especifica el número máximo de estados que admite el algoritmo para un atributo sin secuencia. Si el número de estados que tiene un atributo sin secuencia es mayor que el número máximo de estados, el algoritmo usará los estados más populares del atributo y tratará los restantes como **Missing**.  
  
 El valor predeterminado es 100.  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las siguientes marcas de modelado.  
  
 NOT NULL  
 Indica que la columna no puede contener un valor NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.  
  
 Se aplica a la columna de estructura de minería de datos.  
  
 MODEL_EXISTENCE_ONLY  
 Significa que la columna se tratará como si tuviera dos estados posibles: **Missing** y **Existing**. Un valor NULL se trata como un valor **Missing** .  
  
 Se aplica a la columna de modelo de minería de datos.  
  
 Para obtener más información sobre el uso de valores ausentes en modelos de minería de datos y cómo afectan dichos valores a las puntuaciones de probabilidad, vea [Valores ausentes &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).  
  
## <a name="requirements"></a>Requisitos  
 La tabla de casos debe tener una columna de identificador de caso. Opcionalmente, dicha tabla puede contener otras columnas que almacenen atributos sobre el caso.  
  
 El algoritmo de clústeres de secuencia de Microsoft requiere información de secuencia, almacenada como una tabla anidada. La tabla anidada debe tener una única columna Key Sequence. Una columna **Key Sequence** puede contener cualquier tipo de datos que se puedan ordenar, incluyendo tipos de datos de cadena, pero la columna debe contener valores únicos para cada caso. Es más, antes de procesar el modelo, debe asegurarse de que la tabla de casos y la tabla anidada están ordenadas de manera ascendente por la clave que relaciona las tablas.  
  
> [!NOTE]  
>  Si crea un modelo que usa el algoritmo de clústeres de secuencia de Microsoft pero no emplea una columna de secuencia, el modelo resultante no contendrá ninguna secuencia, sino que simplemente creará clústeres de casos en función de otros atributos incluidos en el modelo.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se enumeran en la tabla siguiente. Para obtener más información sobre lo que significan los tipos de contenido cuando se usan en un modelo de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Continuous, Cyclical, Discrete, Discretized, Key, Key Sequence, Table y Ordered|  
|Atributo de predicción|Continuous, Cyclical, Discrete, Discretized, Table y Ordered|  
  
## <a name="remarks"></a>Comentarios  
  
-   Use la función [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md) para la predicción de secuencias. Para obtener más información sobre las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que admiten la predicción de secuencias, vea [características compatibles con las ediciones de SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
-   El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no admite el uso del lenguaje de marcado de modelos de predicción (PMML) para crear modelos de minería de datos.  
  
-   El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite la obtención de detalles y el uso de modelos de minería de datos OLAP y de dimensiones de minería de datos.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de clústeres de secuencia de Microsoft](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Ejemplos de consultas de modelo de clústeres de secuencia](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Contenido del modelo de minería de datos para modelos de agrupación en clústeres de secuencia & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
