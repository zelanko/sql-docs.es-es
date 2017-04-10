---
title: "Referencia t&#233;cnica del algoritmo de cl&#250;steres de Microsoft | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "clústeres [Minería de datos]"
  - "MAXIMUM_INPUT_ATTRIBUTES, parámetro"
  - "CLUSTER_SEED, parámetro"
  - "MODELLING_CARDINALITY, parámetro"
  - "MINIMUM_SUPPORT, parámetro"
  - "STOPPING_TOLERANCE, parámetro"
  - "MAXIMUM_STATES, parámetro"
  - "SAMPLE_SIZE, parámetro"
  - "CLUSTERING_METHOD, parámetro"
  - "método de agrupación en clústeres blando [Minería de datos]"
  - "algoritmos de clústeres [Analysis Services]"
  - "CLUSTER_COUNT, parámetro"
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
caps.latest.revision: 21
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 21
---
# Referencia t&#233;cnica del algoritmo de cl&#250;steres de Microsoft
  En esta sección se explica la implementación del algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , incluidos los parámetros que se pueden usar para controlar el comportamiento de los modelos de agrupación en clústeres. Además, incluye instrucciones sobre cómo mejorar el rendimiento durante la creación y el procesamiento de modelos de agrupación en clústeres.  
  
 Para obtener información adicional sobre cómo usar los modelos de agrupación en clústeres, vea los temas siguientes:  
  
-   [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [Ejemplos de consultas de modelos de agrupación en clústeres](../../analysis-services/data-mining/clustering-model-query-examples.md)  
  
## Implementar el algoritmo de clústeres de Microsoft  
 El algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] proporciona dos métodos para crear clústeres y asignar puntos de datos a dichos clústeres. El primer método, el algoritmo *mediana-K*, es un método de agrupación en clústeres duro. Esto significa que un punto de datos puede pertenecer a un solo clúster, y que únicamente se calcula una probabilidad de pertenencia de cada punto de datos de ese clúster. El segundo método, *Expectation Maximization* (EM), es un método de *agrupación en clústeres blando*. Esto significa que un punto de datos siempre pertenece a varios clústeres, y que se calcula una probabilidad para cada combinación de punto de datos y clúster.  
  
 Para elegir el algoritmo que prefiere usar, establezca el parámetro *CLUSTERING_METHOD*. El método predeterminado para la agrupación en clústeres es el método EM escalable.  
  
### Agrupación en clústeres EM  
 En el método de agrupación en clústeres EM, el algoritmo refina de forma iterativa un modelo de clústeres inicial para ajustar los datos y determina la probabilidad de que un punto de datos exista en un clúster. El algoritmo finaliza el proceso cuando el modelo probabilístico ajusta los datos. La función usada para determinar el ajuste es el logaritmo de la probabilidad de los datos dado el modelo.  
  
 Si durante el proceso se generan clústeres vacíos, o si la pertenencia de uno o varios de los clústeres cae por debajo del umbral especificado, los clústeres con poblaciones bajas se reinicializan en los nuevos puntos y vuelve a ejecutarse el algoritmo EM.  
  
 Los resultados del método de agrupación en clústeres EM son probabilísticos. Esto significa que cada punto de datos pertenece a todos los clústeres, pero cada asignación de un punto de datos a un clúster tiene una probabilidad diferente. Dado que el método permite que los clústeres se superpongan, la suma de los elementos de todos los clústeres puede superar la totalidad de los elementos existentes en el conjunto de entrenamiento. En los resultados del modelo de minería de datos, las puntuaciones que indican soporte se ajustan para tener en cuenta este hecho.  
  
 El algoritmo EM es el algoritmo predeterminado usado en los modelos de agrupación en clústeres de Microsoft. Este algoritmo se usa como algoritmo predeterminado porque proporciona numerosas ventajas comparado con la agrupación en clústeres mediana-K:  
  
-   Requiere examinar la base de datos como máximo una vez.  
  
-   Funciona incluso si la cantidad de memoria (RAM) es limitada.  
  
-   Tiene la capacidad de usar un cursor de solo avance.  
  
-   Sus resultados superan los obtenidos por los métodos de muestreo.  
  
 La implementación de Microsoft proporciona dos opciones: EM escalable y no escalable. De forma predeterminada, en EM escalable, los primeros 50.000 registros se usan para inicializar el examen inicial. Si esta operación se realiza correctamente, el modelo solo usa estos datos. Si el modelo no se puede ajustar con 50.000 registros, se leen otros 50.000. En EM no escalable, se lee el conjunto de datos completo independientemente de su tamaño. Este método puede crear clústeres más precisos, pero los requisitos de memoria pueden ser significativos. Dado que EM escalable funciona en un búfer local, recorrer los datos en iteración es mucho más rápido, y el algoritmo hace un mejor uso de la caché de memoria de la CPU que EM no escalable. Es más, EM escalable es tres veces más rápido que EM no escalable, incluso si todos los datos caben en la memoria principal. En la mayoría de casos, la mejora en el rendimiento no significa una reducción de la calidad del modelo completo.  
  
 Para consultar un informe técnico donde se describe la implementación de EM en el algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)], vea [Scaling EM (Expectation Maximization) Clustering to Large Databases](http://go.microsoft.com/fwlink/?LinkId=45964) (Escalado de agrupación en clústeres de EM [Expectation Maximization] en bases de datos de gran tamaño).  
  
### Agrupación en clústeres mediana-K  
 La agrupación en clústeres mediana-K es un método muy conocido para asignar la pertenencia al clúster que consiste en minimizar las diferencias entre los elementos de un clúster al tiempo que se maximiza la distancia entre los clústeres. El término “mediana” en mediana-K hace referencia al *centroide* del clúster, que es un punto de datos que se elige arbitrariamente y que se restringe de forma iterativa hasta que representa la media real de todos los puntos de datos del clúster. La "K" hace referencia a un número arbitrario de puntos que se usan para inicializar el proceso de agrupación en clústeres. El algoritmo mediana-K calcula las distancias euclidianas cuadradas entre los registros de datos de un clúster y el vector que representa la media de clústeres, y converge en un conjunto final de K clústeres cuando la suma alcanza su valor mínimo.  
  
 El algoritmo mediana-K asigna cada punto de datos a un solo clúster y no permite la incertidumbre en la pertenencia. En un clúster, la pertenencia se expresa como una distancia desde el centroide.  
  
 Normalmente, el algoritmo mediana-K se usa para crear clústeres de atributos continuos, donde el cálculo de la distancia a una media se realiza de manera sencilla. Sin embargo, la implementación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] adapta el método mediana-K a atributos discretos de clúster mediante el uso de probabilidades.  Para los atributos discretos, la distancia de un punto de datos desde un clúster determinado se calcula de la manera siguiente:  
  
 1 - P(punto de datos, clúster)  
  
> [!NOTE]  
>  El algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no expone la función de distancia usada para calcular la mediana-K, y las medidas de la distancia no están disponibles en el modelo completado. Sin embargo, se puede utilizar una función de predicción para devolver un valor que corresponda a la distancia, donde la distancia se calcula como la probabilidad de que un punto de datos pertenezca al clúster. Para más información, vea [ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md).  
  
 El algoritmo mediana-K proporciona dos métodos para realizar un muestreo en el conjunto de datos: mediana-K no escalable, que carga el conjunto de datos completo y realiza una pasada de agrupación en clústeres, y mediana-K escalable, donde el algoritmo usa los primeros 50.000 casos y lee más casos únicamente si necesita más datos para lograr un buen ajuste del modelo a los datos.  
  
### Actualizaciones al algoritmo de clústeres de Microsoft en SQL Server 2008  
 En SQL Server 2008, la configuración predeterminada del algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] se ha cambiado para usar el parámetro interno, NORMALIZATION = 1. La normalización se lleva a cabo usando estadísticas de puntuación-z y se supone una distribución normal. El propósito de este cambio en el comportamiento predeterminado es minimizar el efecto de los atributos que puedan tener grandes magnitudes y muchos valores atípicos. Sin embargo, la normalización puntuación-z puede alterar los resultados de la agrupación en clústeres en distribuciones que no son normales (como las distribuciones uniformes). Para evitar la normalización y obtener el mismo comportamiento que el algoritmo de clústeres mediana-K de SQL Server 2005, puede usar el cuadro de diálogo **Configuración de parámetros** para agregar el parámetro personalizado (NORMALIZATION) y establecer su valor en 0.  
  
> [!NOTE]  
>  El parámetro NORMALIZATION es una propiedad interna del algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] y no es compatible. En general, el uso de la normalización se recomienda en los modelos de agrupación en clústeres para mejorar el resultado del modelo.  
  
## Personalizar el algoritmo de clústeres de Microsoft  
 El algoritmo de clústeres [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite varios parámetros que afectan al comportamiento, el rendimiento y la precisión del modelo de minería de datos resultante.  
  
### Establecer parámetros del algoritmo  
 En la tabla siguiente se describen los parámetros que se pueden usar con el algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Estos parámetros afectan tanto al rendimiento como a la precisión del modelo de minería de datos resultante.  
  
 CLUSTERING_METHOD  
 Especifica el método de agrupación en clústeres que va a usar el algoritmo. Los métodos de agrupación en clústeres disponibles son:  
  
|ID|Método|  
|--------|------------|  
|1|EM escalable|  
|2|EM no escalable|  
|3|Mediana-K escalable|  
|4|Mediana-K no escalable.|  
  
 El valor predeterminado es 1 (EM escalable).  
  
 CLUSTER_COUNT  
 Especifica el número aproximado de clústeres que generará el algoritmo. Si no se puede generar el número aproximado de clústeres a partir de los datos, el algoritmo genera tantos clústeres como sea posible. Si CLUSTER_COUNT se establece en 0, el algoritmo utiliza la heurística para determinar el mejor número de clústeres que debe generar.  
  
 El valor predeterminado es 10.  
  
 CLUSTER_SEED  
 Especifica el número de inicialización usado para generar clústeres aleatoriamente para la fase inicial de generación del modelo.  
  
 Cambiando este número, se puede cambiar la manera en que se generan los clústeres iniciales y, a continuación, comparar modelos que se han generado usando inicializaciones diferentes. Si se cambia la inicialización pero los clústeres hallados no cambian en gran medida, el modelo se puede considerar relativamente estable.  
  
 El valor predeterminado es 0.  
  
 MINIMUM_SUPPORT  
 Especifica el número mínimo de casos requeridos para generar un clúster. Si el número de casos del clúster es inferior a este número, el clúster se trata como vacío y se descarta.  
  
 Si se establece un número demasiado alto, se pueden perder clústeres válidos.  
  
> [!NOTE]  
>  Si se usa EM, que es el método de agrupación en clústeres predeterminado, algunos clústeres pueden tener un valor de soporte más bajo que el valor especificado. Esto se debe a que cada caso se evalúa según su pertenencia a todos los clústeres posibles, y para algunos clústeres puede haber solo un soporte mínimo.  
  
 El valor predeterminado es 1.  
  
 MODELLING_CARDINALITY  
 Especifica el número de modelos de ejemplo que se generan durante el proceso de agrupación en clústeres.  
  
 Reducir el número de modelos candidatos puede mejorar el rendimiento, pero se corre el riesgo de perder algunos modelos buenos.  
  
 El valor predeterminado es 10.  
  
 STOPPING_TOLERANCE  
 Especifica el valor que se usa para determinar cuándo se alcanza la convergencia y el algoritmo termina de generar el modelo. La convergencia se alcanza cuando el cambio general de las probabilidades del clúster es inferior al resultado de dividir el parámetro STOPPING_TOLERANCE entre el tamaño del modelo.  
  
 El valor predeterminado es 10.  
  
 SAMPLE_SIZE  
 Especifica el número de casos que usa el algoritmo en cada paso si el parámetro CLUSTERING_METHOD está establecido en uno de los métodos de agrupación en clústeres escalables. Si establece el parámetro SAMPLE_SIZE en 0, todo el conjunto de datos se agrupará en un único paso. Cargar el conjunto de datos completo en un paso único puede causar problemas de memoria y de rendimiento.  
  
 El valor predeterminado es 50000.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Especifica el número máximo de atributos de entrada que el algoritmo puede procesar antes de invocar la selección de características. Si se establece este valor en 0, se especifica que no existe un número máximo de atributos.  
  
 Aumentar el número de atributos puede degradar significativamente el rendimiento.  
  
 El valor predeterminado es 255.  
  
 MAXIMUM_STATES  
 Especifica el número máximo de estados de atributo que admite el algoritmo. Si un atributo tiene más estados que el máximo permitido, el algoritmo usa los estados más conocidos y pasa por alto los estados restantes.  
  
 Aumentar el número de estados puede degradar significativamente el rendimiento.  
  
 El valor predeterminado es 100.  
  
### Marcas de modelado  
 El algoritmo admite las marcas de modelado que se indican a continuación. Los marcadores de modelado se definen al crear la estructura de minería de datos o el modelo de minería de datos. Las marcas de modelado especifican cómo se procesan los valores de cada columna durante el análisis.  
  
|Marca de modelado|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|La columna se tratará como si tuviera dos estados posibles: ausente y existente. Un valor NULL es un valor ausente.<br /><br /> Se aplica a la columna del modelo de minería de datos.|  
|NOT NULL|La columna no puede contener valores NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.<br /><br /> Se aplica a la columna de la estructura de minería de datos.|  
  
## Requisitos  
 Un modelo de agrupación en clústeres debe contener una columna de clave y columnas de entrada. También se pueden definir columnas de entrada como columnas de predicción. Las columnas establecidas en **Predict Only** no se usan para generar clústeres. La distribución de estos valores en los clústeres se calcula después de que se hayan generado los clústeres.  
  
### Columnas de entrada y de predicción  
 El algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se enumeran en la tabla siguiente. Para más información sobre el significado de los tipos de contenido usados en un modelo de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Continuous, Cyclical, Discrete, Discretized, Key, Table, Ordered|  
|Atributo de predicción|Continuous, Cyclical, Discrete, Discretized, Table, Ordered|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido Cyclical y Ordered, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## Vea también  
 [Algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)   
 [Ejemplos de consultas de modelos de agrupación en clústeres](../../analysis-services/data-mining/clustering-model-query-examples.md)   
 [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  