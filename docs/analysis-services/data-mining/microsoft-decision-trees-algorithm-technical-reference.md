---
title: "Referencia técnica del algoritmo de árboles de decisión de Microsoft | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c098b5144a06cae6afb5b79ca4bf395a68768bd3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Referencia técnica del algoritmo de árboles de decisión de Microsoft
  El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo híbrido que incorpora distintos métodos para crear un árbol, y admite varias tareas de análisis, incluyendo la regresión, la clasificación y la asociación. El algoritmo de árboles de decisión de Microsoft admite el modelado de los atributos discretos y continuos.  
  
 En este tema se explica la implementación del algoritmo, se describe cómo personalizar su comportamiento para distintas tareas y se proporcionan vínculos a información adicional sobre cómo consultar los modelos de árboles de decisión.  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>Implementación del algoritmo de árboles de decisión  
 El algoritmo de árboles de decisión de Microsoft aplica el enfoque bayesiano en el aprendizaje de los modelos de interacción causales al obtener las distribuciones posteriores aproximadas de los modelos. Para obtener una explicación detallada de este enfoque, consulte el documento en el sitio de Microsoft Research sobre el [aprendizaje de la estructura y parámetros](http://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409).  
  
 La metodología para evaluar el valor de la información de las *prioridades* necesarias para el aprendizaje se basa en el supuesto de *equivalencia de probabilidad*. Este supuesto establece que los datos no deberían ayudar a discriminar estructuras de red que, de otro modo, representarían las mismas aserciones de independencia condicional. Se supone que cada caso tiene una única red bayesiana anterior y una única medida de confianza para dicha red.  
  
 Mediante estas redes anteriores, el algoritmo calcula las *probabilidades posteriores* relativas de las estructuras de red dados los datos de entrenamiento actuales, e identifica las estructuras de red con las probabilidades posteriores más altas.  
  
 El algoritmo de árboles de decisión de Microsoft usa distintos métodos para calcular el mejor árbol. El método usado dependerá de la tarea, que puede ser la regresión lineal, la clasificación o el análisis de la asociación. Un solo modelo puede contener varios árboles para distintos atributos de predicción. Es más, cada árbol puede contener varias bifurcaciones, dependiendo del número de atributos y de valores que contienen los datos. La forma y profundidad del árbol integrado en un modelo determinado depende del método de puntuación y del resto de parámetros usados. Los cambios en los parámetros también pueden afectar al lugar donde se dividen los nodos.  
  
### <a name="building-the-tree"></a>Generar el árbol  
 Cuando el algoritmo de árboles de decisión de Microsoft crea el conjunto de posibles valores de entrada, realiza una *feature selection* para identificar los atributos y los valores que ofrecen la mayor cantidad de información, y no tiene en cuenta los valores que son muy raros. El algoritmo también agrupa los valores en *bandejas*para crear agrupaciones de valores que se pueden procesar como una unidad para optimizar el rendimiento.  
  
 Un árbol se genera mediante la determinación de las correlaciones entre una entrada y el resultado deseado. Una vez correlacionados todos los atributos, el algoritmo identifica el atributo único que separa más claramente los resultados. Este punto de la mejor separación se mide usando una ecuación que calcula la obtención de información. El atributo que tiene la mejor puntuación para la obtención de información se usa para dividir los casos en subconjuntos, que posteriormente son analizados de forma recursiva por el mismo proceso hasta que no sea posible dividir más el árbol.  
  
 La ecuación exacta empleada para evaluar la obtención de información depende de los parámetros establecidos al crear el algoritmo, del tipo de datos de la columna de predicción y del tipo de datos de la entrada.  
  
### <a name="discrete-and-continuous-inputs"></a>Entradas discretas y continuas  
 Cuando tanto el atributo de predicción como las entradas son discretas, el recuento de los resultados por entrada se realizará creando una matriz y generando puntuaciones para cada celda de la matriz.  
  
 Sin embargo, cuando el atributo de predicción es discreto y las entradas son continuas, la entrada de las columnas continuas se discretiza automáticamente. Puede aceptar los valores predeterminados para que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determine el número óptimo de agrupaciones, o bien puede controlar la forma en que las entradas continuas se discretizan si establece las propiedades <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> . Para más información, vea [Cambiar la discretización de una columna en un modelo de minería de datos](../../analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md).  
  
 Para los atributos continuos, el algoritmo usa la regresión lineal para determinar dónde se divide un árbol de decisión.  
  
 Cuando el atributo de predicción es un tipo de datos numéricos continuo, la selección de características también se aplica a las salidas para reducir el número de resultados posibles y generar más rápidamente el modelo. Puede cambiar el umbral para la selección de características, incrementando o disminuyendo de esta manera el número de valores posibles, estableciendo el parámetro MAXIMUM_OUTPUT_ATTRIBUTES.  
  
 Para obtener una explicación más detallada acerca de cómo funciona el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] con columnas de predicción discretas, vea el artículo sobre [Descripción de las redes bayesianas: combinación de conocimiento y datos estadísticos](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf). Para más información sobre cómo funciona el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] con una columna de predicción continua, vea el apéndice del artículo [Autoregressive Tree Models for Time-Series Analysis](http://go.microsoft.com/fwlink/?LinkId=45966)(Modelos de árbol de regresión automática para el análisis de series temporales).  
  
### <a name="scoring-methods-and-feature-selection"></a>Métodos de puntuación y selección de características  
 El algoritmo de árboles de decisión de Microsoft proporciona tres fórmulas para puntuar la obtención de información: la entropía de Shannon, la red bayesiana con prioridad K2 y la red bayesiana con una distribución Dirichlet uniforme de prioridades. Los tres métodos están bien consolidados en el campo de la minería de datos. Se recomienda que experimente con parámetros y métodos de puntuación diferentes para determinar cuáles son los que proporcionan mejores resultados. Para obtener más información acerca de estos métodos de puntuación, vea [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
 Todos los algoritmos de minería de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usan automáticamente la selección de características para mejorar el análisis y reducir la carga de procesamiento. El método usado para la selección de características depende del algoritmo empleado para generar el modelo. Los parámetros del algoritmo que controlan la selección de características para el modelo de árboles de decisión son MAXIMUM_INPUT_ATTRIBUTES y MAXIMUM_OUTPUT.  
  
|Algoritmo|Método de análisis|Comentarios|  
|---------------|------------------------|--------------|  
|Árboles de decisión|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|Si alguna columna contiene valores continuos no binarios, se utiliza la puntuación interestingness (grado de interés) en todas las columnas para asegurar la coherencia. En caso contrario, se utiliza el método predeterminado o el especificado.|  
|Regresión lineal|Puntuación interestingness|La regresión lineal solo utiliza la puntuación interestingness porque solo admite columnas continuas.|  
  
### <a name="scalability-and-performance"></a>Escalabilidad y rendimiento  
 La clasificación es una estrategia de minería de datos importante. Generalmente, la cantidad de información necesaria para clasificar los casos crece en proporción directa al número de registros de entrada. Esto limita el tamaño de los datos que se pueden clasificar. El algoritmo de árboles de decisión de Microsoft usa los métodos siguientes para resolver estos problemas, mejorar el rendimiento y eliminar las restricciones de memoria:  
  
-   Selección de características para optimizar la selección de atributos.  
  
-   Puntuación bayesiana para controlar el crecimiento del árbol.  
  
-   Optimización de bandejas para los atributos continuos.  
  
-   Agrupación dinámica de valores de entrada para determinar los valores más importantes.  
  
 El algoritmo de árboles de decisión de Microsoft es rápido y escalable, y se ha diseñado para ser usado en paralelo, es decir, con todos los procesadores funcionando juntos para generar un modelo único y coherente. La combinación de estas características convierte al clasificador de árboles de decisión en una herramienta ideal para la minería de datos.  
  
 Si las restricciones de rendimiento son graves, podría mejorar el tiempo de procesamiento durante el entrenamiento de un modelo de árbol de decisión usando los métodos siguientes. Sin embargo, si lo hace, tenga en cuenta que la eliminación de atributos para mejorar el rendimiento del procesamiento cambiará los resultados del modelo, y es posible que éste sea menos representativo de la población total.  
  
-   Aumente el valor del parámetro COMPLEXITY_PENALTY para limitar el crecimiento del árbol.  
  
-   Limite el número de elementos de los modelos de asociación para limitar el número de árboles que se generan.  
  
-   Aumente el valor del parámetro MINIMUM_SUPPORT para evitar el sobreajuste.  
  
-   Restrinja a 10 o menos el número de valores discretos para todos los atributos. Puede intentar agrupar valores de distintas maneras en modelos diferentes.  
  
    > [!NOTE]  
    >  Puede utilizar las herramientas de exploración de datos disponibles en  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] para visualizar la distribución de valores en los datos y agrupar de forma apropiada dichos valores antes de comenzar la minería de datos. Para más información, vea [Tarea de generación de perfiles de datos y Visor](../../integration-services/control-flow/data-profiling-task-and-viewer.md). También puede usar los [complementos de minería de datos para Excel 2007](http://www.microsoft.com/downloads/details.aspx?FamilyID=7C76E8DF-8674-4C3B-A99B-55B17F3C4C51)para explorar y agrupar datos en Microsoft Excel, así como para cambiar sus etiquetas.  
  
## <a name="customizing-the-decision-trees-algorithm"></a>Personalizar el algoritmo de árboles de decisión  
 El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite parámetros que afectan al rendimiento y la precisión del modelo de minería de datos resultante. También puede establecer marcas de modelado en las columnas del modelo de minería de datos o de la estructura de minería de datos para controlar la manera en que se procesan los datos.  
  
> [!NOTE]  
>  El algoritmo de árboles de decisión de Microsoft está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; sin embargo, algunos parámetros avanzados para personalizar el comportamiento de dicho algoritmo pueden usarse exclusivamente en ciertas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2012](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473).  
  
### <a name="setting-algorithm-parameters"></a>Establecer parámetros del algoritmo  
 En la tabla siguiente se describen los parámetros que puede usar con el algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 *COMPLEXITY_PENALTY*  
 Controla el crecimiento del árbol de decisión. Un valor bajo aumenta el número de divisiones y un valor alto lo reduce. El valor predeterminado se basa en el número de atributos de un modelo concreto, como se describe en la lista siguiente:  
  
-   De 1 a 9 atributos, el valor predeterminado es 0,5.  
  
-   De 10 a 99 atributos, el valor predeterminado es 0,9.  
  
-   Para 100 o más atributos, el valor predeterminado es 0,99.  
  
 *FORCE_REGRESSOR*  
 Fuerza al algoritmo a utilizar las columnas indicadas como regresores, independientemente de su importancia según los cálculos del algoritmo. Este parámetro sólo se usa para árboles de decisión que predicen un atributo continuo.  
  
> [!NOTE]  
>  Establezca este parámetro si desea que el algoritmo intente usar el atributo como un regresor. Sin embargo, el atributo se usará realmente como regresor en el modelo final en función de los resultados del análisis. Para averiguar las columnas que se usaron como regresores, consulte el contenido del modelo.  
  
 [Disponible solo en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 Define el número de atributos de entrada que el algoritmo puede controlar antes de invocar la selección de características.  
  
 El valor predeterminado es 255.  
  
 Establezca este valor en 0 para desactivar la selección de características.  
  
 [Disponible solo en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 Define el número de atributos de salida que el algoritmo puede controlar antes de invocar la selección de características.  
  
 El valor predeterminado es 255.  
  
 Establezca este valor en 0 para desactivar la selección de características.  
  
 [Disponible solo en algunas ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
  
 *MINIMUM_SUPPORT*  
 Determina el número mínimo de casos de hoja necesarios para generar una división en el árbol de decisión.  
  
 El valor predeterminado es 10.  
  
 Es posible que necesite aumentar este valor si el conjunto de datos es muy grande, para evitar el sobreentrenamiento.  
  
 *SCORE_METHOD*  
 Determina el método usado para calcular el resultado de la división. Las siguientes opciones están disponibles:  
  
|Id.|Nombre|  
|--------|----------|  
|1|Entropía|  
|3|Bayesiano con prioridad K2|  
|4|Equivalente Dirichlet bayesiano (BDE) con prioridad uniforme<br /><br /> (predeterminado).|  
  
 El valor predeterminado es 4 o BDE.  
  
 Para obtener una explicación de estos métodos de puntuación, vea [Feature Selection](http://msdn.microsoft.com/library/73182088-153b-4634-a060-d14d1fd23b70).  
  
 *SPLIT_METHOD*  
 Determina el método usado para dividir el nodo. Las siguientes opciones están disponibles:  
  
|Id.|Nombre|  
|--------|----------|  
|1|**Binary:** indica que, independientemente del número real de valores para el atributo, el árbol se debería dividir en dos bifurcaciones.|  
|2|**Complete:** indica que el árbol puede crear tantas divisiones como valores de atributo existan.|  
|3|**Both:** especifica que Analysis Services puede determinar si se debe usar una división binaria o completa para generar los mejores resultados.|  
  
 El valor predeterminado es 3.  
  
### <a name="modeling-flags"></a>Marcadores de modelado  
 El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las marcas de modelado siguientes. Al crear la estructura o el modelo de minería de datos, se definen las marcas de modelado que especifican cómo se tratan los valores de cada columna durante el análisis. Para obtener más información, vea [Marcas de modelado &#40;Minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md).  
  
|Marca de modelado|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|Significa que la columna se tratará como si tuviera dos estados posibles: **Missing** y **Existing**. Un valor NULL es un valor ausente.<br /><br /> Se aplica a las columnas del modelo de minería de datos.|  
|NOT NULL|Indica que la columna no puede contener un valor NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.<br /><br /> Se aplica a las columnas de la estructura de minería de datos.|  
  
### <a name="regressors-in-decision-tree-models"></a>Regresores en modelos de árbol de decisión  
 Aun cuando no use el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , cualquier modelo de árbol de decisión que tenga entradas y salidas numéricas continuas puede incluir nodos que representan una regresión en un atributo continuo.  
  
 No es necesario especificar que una columna de datos numéricos continuos representa un regresor. El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] usará automáticamente la columna como un regresor potencial y dividirá el conjunto de datos en regiones con patrones significativos aunque no se establezca la marca REGRESSOR en la columna.  
  
 Sin embargo, puede usar el parámetro FORCE_REGRESSOR para garantizar que el algoritmo empleará un regresor determinado. Este parámetro solo se puede usar con los algoritmos de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] y de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Al establecer la marca de modelado, el algoritmo intentará buscar ecuaciones de regresión con el formato `a*C1 + b*C2 + ...` que se ajusten a los patrones de los nodos del árbol. Se calcula la suma de los valores residuales y, si la desviación es demasiado grande, se fuerza una división en el árbol.  
  
 Por ejemplo, si está prediciendo los hábitos de compra de los clientes usando **Income** como atributo y ha establecido la marca de modelado REGRESSOR en la columna, el algoritmo intentará en primer lugar ajustar los valores de **Income** mediante una fórmula de regresión estándar. Si la desviación es demasiado grande, se abandona la fórmula de regresión y el árbol se dividirá de acuerdo con otro atributo. A continuación, el algoritmo de árboles de decisión intentará ajustar un regresor para los ingresos en cada una de las ramas después de la división.  
  
## <a name="requirements"></a>Requisitos  
 Un modelo de árbol de decisión debe contener una columna de clave, columnas de entrada y al menos una columna de predicción.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo de árboles de decisión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se incluyen en la tabla siguiente. Para más información sobre lo que significan los tipos de contenido cuando se usan en un modelo de minería de datos, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md).  
  
|Columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Continuous, Cyclical, Discrete, Discretized, Key, Ordered, Table|  
|Atributo de predicción|Continuous, Cyclical, Discrete, Discretized, Ordered, Table|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido Cyclical y Ordered, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de árboles de decisión de Microsoft](../../analysis-services/data-mining/microsoft-decision-trees-algorithm.md)   
 [Ejemplos de consultas de modelo de árboles de decisión](../../analysis-services/data-mining/decision-trees-model-query-examples.md)   
 [Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
