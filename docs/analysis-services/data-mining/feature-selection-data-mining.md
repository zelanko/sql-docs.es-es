---
title: (Minería de datos) de la selección de características | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a93e503978779e56250ddf190c61b1b2411050b9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="feature-selection-data-mining"></a>Selección de características (minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La *selección de características* es una parte importante del aprendizaje automático. La selección de características hace referencia al proceso de reducir las entradas para su procesamiento y análisis, o de encontrar las entradas más significativas. Un término relacionado, *ingeniería de características* (o *extracción de características*), hace referencia al proceso de extraer información útil o características de datos existentes.  
  
## <a name="why-do-feature-selection"></a>¿Por qué usar la selección de características?  
 La selección de características es crítica para crear un modelo adecuado por varios motivos. El primero motivo es que la selección de características implica cierto grado de *reducción de cardinalidad*para imponer un corte en el número de atributos que se tendrán en cuenta al crear un modelo. Los datos casi siempre contienen más información de la necesaria para crear el modelo, o bien el tipo incorrecto de información. Por ejemplo, puede que tenga un conjunto de datos de 500 columnas donde se describan las características de los clientes. Pero, si algunas de las columnas tienen pocos datos, obtendrá pocas ventajas si las agrega al modelo y, si algunas de las columnas están duplicadas, usar las dos columnas podría afectar al modelo.  
  
 La selección de características no solo mejora la calidad del modelo, sino que también hace que el proceso de modelado sea más eficiente. Si usa columnas innecesarias al generar el modelo, se necesitará más CPU y memoria durante el proceso de entrenamiento, así como más espacio de almacenamiento para el modelo completado. Incluso si los recursos no son un problema, se recomienda realizar la selección de características para identificar las mejores columnas, ya que las columnas innecesarias pueden reducir la calidad del modelo de varias formas:  
  
-   Los datos redundantes o poco relevantes hacen que resulte más difícil detectar patrones significativos.  
  
-   Si el conjunto de datos es de dimensiones elevadas, la mayoría de los algoritmos de minería de datos necesitarán un conjunto de datos de aprendizaje mucho más grande.  
  
 Durante el proceso de selección de características, el analista, la herramienta de modelado o el algoritmo seleccionan o descartan de forma activa atributos según su utilidad para el análisis.  El analista puede usar la ingeniería de características para agregar características y quitar o modificar datos existentes, mientras que el algoritmo de aprendizaje automático suele asignar puntuaciones a las columnas y valida su utilidad en el modelo.  
  
 ![Característica de selección y el proceso de ingeniería](../../analysis-services/data-mining/media/ssdm-featureselectionprocess.png "selección y el proceso de ingeniería de características")  
  
 En resumen, la selección de características ayuda a solucionar dos problemas: tener demasiados datos de escaso valor, o bien tener muy pocos datos de mucho valor. Su objetivo en la selección de características sería identificar el número mínimo de columnas del origen de datos que son significativas para crear un modelo.  
  
## <a name="how-feature-selection-works-in-sql-server-data-mining"></a>Funcionamiento de la selección de características en la minería de datos de SQL Server  
 La selección de características siempre se realiza antes de entrenar el modelo. Con algunos algoritmos, las técnicas de selección de características están "integradas", de forma que las columnas irrelevantes se excluyen y se identifican automáticamente las mejores características. Cada algoritmo tiene su propio conjunto de técnicas predeterminadas para aplicar de forma inteligente la reducción de características.  Sin embargo, también puede establecer parámetros manualmente para influir en el comportamiento de la selección de características.  
  
 Durante la selección automática de características, se calcula una puntuación para cada atributo y se seleccionan los atributos que tengan las mejores puntuaciones para el modelo. También puede ajustar el umbral para las puntuaciones más altas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La minería de datos proporciona varios métodos para calcular estas puntuaciones y el método exacto que se aplica en un modelo depende de estos factores:  
  
-   El algoritmo usado en el modelo  
  
-   El tipo de datos del atributo  
  
-   Otros parámetros que se hayan podido establecer en el modelo  
  
 La selección de características se aplica a las entradas, a los atributos de predicción o a los estados de una columna. Una vez completada la puntuación para la selección de características, solo se incluyen en el proceso de generación del modelo y se pueden usar en la predicción los atributos y los estados que selecciona el algoritmo. Si elige un atributo de predicción que no alcanza el umbral para la selección de características, dicho atributo se puede usar en la predicción, pero las predicciones se basarán únicamente en las estadísticas globales que existen en el modelo.  
  
> [!NOTE]  
>  La selección de características afecta solo a las columnas que se usan en el modelo y no tiene ningún efecto en el almacenamiento de la estructura de minería de datos. Las columnas que se dejan fuera del modelo de minería de datos siguen estando disponibles en la estructura, y los datos de las columnas de la estructura de minería de datos se almacenan en caché.  
  
### <a name="feature-selection-scores"></a>Puntuaciones de selección de características  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La minería de datos es compatible con estos métodos comunes y estandarizados para asignar puntuaciones a los atributos. El método específico usado en un conjunto de datos o algoritmo concretos depende de los tipos de datos y del uso de las columnas.  
  
-   La puntuación *interestingness* (medida del interés) se usa para clasificar y ordenar los atributos de las columnas que contienen datos numéricos continuos no binarios.  
  
-   La*entropía de Shannon* y dos puntuaciones *bayesianas* están disponibles para las columnas que contengan datos discretos y discretizados. Sin embargo, si el modelo contiene columnas continuas, se usará la puntuación de grado de interés para evaluar todas las columnas de entrada, con objeto de asegurarse de que son coherentes.  
  
#### <a name="interestingness-score"></a>Puntuación interestingness  
 Una característica es interesante si ofrece información útil. Pero el *grado de interés* se puede medir de varias formas.  El método de*novedades* puede ser útil para detectar valores atípicos, pero la capacidad para diferenciar entre elementos estrechamente relacionados (o *diferenciar su importancia*) podría resultar más interesante para la clasificación.  
  
 La medida del grado de interés que se usa en la minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está *basada en la entropía*, lo que significa que los atributos con distribuciones aleatorias tienen una entropía más alta y obtienen menos información (y, por lo tanto, esos atributos son menos interesantes). La entropía para cualquier atributo se compara con la entropía de todos los demás atributos de la manera siguiente:  
  
 Interestingness(Atributo) = - (m - Entropy(Atributo)) * (m - Entropy(Atributo))  
  
 La entropía central (o m) es la entropía de todo el conjunto de características. Al restar la entropía del atributo de destino de la entropía central, se puede evaluar cuánta información proporciona el atributo.  
  
 Esta puntuación se utiliza de forma predeterminada cada vez que la columna contiene datos numéricos continuos no binarios.  
  
#### <a name="shannons-entropy"></a>entropía de Shannon  
 La entropía de Shannon mide la incertidumbre de una variable aleatoria para un determinado resultado. Por ejemplo, la entropía de lanzar una moneda al aire para decidir algo a cara o cruz se puede representar como una función de la probabilidad de que salga cara.  
  
 Analysis Services usa la fórmula siguiente para calcular la entropía de Shannon:  
  
 H(X) = -∑ P(xi) log(P(xi))  
  
 Este método de puntuación está disponible para los atributos discretos y de datos discretos.  
  
#### <a name="bayesian-with-k2-prior"></a>Bayesiano con prioridad K2  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] La minería de datos proporciona dos puntuaciones de selección de características basadas en las redes bayesianas. Una red bayesiana es un gráfico *dirigido* o *acíclico* de estados y de transiciones entre ellos; esto significa que algunos estados siempre son anteriores al estado actual y otros son posteriores, y que el gráfico no se repite ni realiza bucles. Por definición, las redes bayesianas permiten el uso del conocimiento previo. Sin embargo, la pregunta sobre qué estados anteriores se deben utilizar para calcular las probabilidades de los estados posteriores es importante para la precisión, el rendimiento y el diseño del algoritmo.  
  
 Cooper y Herskovits desarrollaron el algoritmo K2 para el aprendizaje a partir de una red bayesiana y este algoritmo se utiliza a menudo en la minería de datos. Es escalable y puede analizar varias variables, pero requiere la ordenación de las variables utilizadas como entrada. Para obtener más información, vea el documento [Learning Bayesian Networks](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf) por Chickering, Geiger y Heckerman.  
  
 Este método de puntuación está disponible para los atributos discretos y de datos discretos.  
  
#### <a name="bayesian-dirichlet-equivalent-with-uniform-prior"></a>Equivalente Dirichlet bayesiano con prioridad uniforme  
 La puntuación Equivalente Dirichlet bayesiano (BDE) también utiliza el análisis bayesiano para evaluar una red dado un conjunto de datos. El método de puntuación BDE fue desarrollado por Heckerman y está basado en la métrica BD desarrollada por Cooper y Herskovits. La distribución Dirichlet es una distribución multinomial que describe la probabilidad condicional de cada variable de la red y dispone de muchas propiedades que son útiles para el aprendizaje.  
  
 El método Equivalente Dirichlet bayesiano con prioridad uniforme (BDEU) considera un caso especial de la distribución Dirichlet, en el que se utiliza una constante matemática para crear una distribución fija o uniforme de estados anteriores. La puntuación BDE también considera la equivalencia de probabilidad; esto significa que no es de esperar que los datos diferencien estructuras equivalentes. Es decir, si la puntuación de “Si A, entonces B” es la misma que la puntuación de “Si B, entonces A”, las estructuras no se pueden diferenciar basándose en los datos y no se puede deducir la causalidad.  
  
 Para obtener más información sobre las redes bayesianas y la implementación de estos métodos de puntuación, vea este artículo sobre las [redes bayesianas](http://research.microsoft.com/en-us/um/people/heckerman/hgc94uai.pdf).  
  
### <a name="feature-selection-methods-per-algorithm"></a>Métodos de selección de características por algoritmo  
 La tabla siguiente contiene una lista de los algoritmos que admiten la selección de características, los métodos de selección de características utilizados por los algoritmos, y los parámetros que se establecen para controlar el comportamiento de la selección de características.  
  
|Algoritmo|Método de análisis|Comentarios|  
|---------------|------------------------|--------------|  
|Bayes naive|entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|El algoritmo Bayes naive de Microsoft solo acepta atributos discretos o de datos discretos, por lo que no puede utilizar la puntuación interestingness.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Naive Bayes Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm-technical-reference.md).|  
|Árboles de decisión|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|Si alguna columna contiene valores continuos no binarios, se utiliza la puntuación interestingness (grado de interés) en todas las columnas para asegurar la coherencia. De lo contrario, se usa el método de selección de características predeterminado o el método que se haya especificado al crear el modelo.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Decision Trees Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md).|  
|Red neuronal|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|El algoritmo de redes neuronales de Microsoft puede usar el método bayesiano y el método basado en la entropía, siempre y cuando los datos contengan columnas continuas.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Neural Network Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md).|  
|Regresión logística|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|Aunque el algoritmo de regresión logística de Microsoft se basa en el algoritmo de red neuronal de Microsoft, no se pueden personalizar los modelos de regresión logística para controlar el comportamiento de la selección de características; por lo tanto, la selección de características siempre usa de manera predeterminada el método más apropiado para el atributo.<br /><br /> Si todos los atributos son discretos o de datos discretos, el valor predeterminado es BDEU.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Logistic Regression Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-logistic-regression-algorithm-technical-reference.md).|  
|Agrupación en clústeres|Puntuación interestingness|El algoritmo de clústeres de Microsoft puede usar datos discretos o discretizados. Sin embargo, dado que la puntuación de cada atributo se calcula como una distancia y se representa como un número continuo, se debe usar la puntuación interestingness.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).|  
|Regresión lineal|Puntuación interestingness|El algoritmo de regresión lineal de Microsoft solo puede usar la puntuación interestingness porque solamente admite columnas continuas.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Linear Regression Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md).|  
|Reglas de asociación<br /><br /> Agrupación en clústeres de secuencia|No se utiliza|La selección de características no se invoca con estos algoritmos.<br /><br /> Sin embargo, se puede controlar el comportamiento del algoritmo y reducir el tamaño de los datos de entrada, si es necesario, al establecer el valor de los parámetros MINIMUM_SUPPORT y MINIMUM_PROBABILITY.<br /><br /> Para obtener más información, consulte [Microsoft Association Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md) y [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).|  
|Serie temporal|No se utiliza|La selección de características no se aplica a los modelos de serie temporal.<br /><br /> Para obtener más información acerca de este algoritmo, vea [Microsoft Time Series Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md).|  
  
## <a name="feature-selection-parameters"></a>Parámetros de selección de características  
 En los algoritmos que admiten la selección de características se puede controlar cuándo se encuentra activada dicha selección usando los parámetros siguientes. Cada algoritmo tiene un valor predeterminado para el número de entradas permitidas, pero se puede invalidar este valor y especificar el número de atributos. En esta sección se enumeran los parámetros que se proporcionan para administrar la selección de características.  
  
#### <a name="maximuminputattributes"></a>MAXIMUM_INPUT_ATTRIBUTES  
 Si un modelo contiene más columnas que el número especificado en el parámetro *MAXIMUM_INPUT_ATTRIBUTES* , el algoritmo pasa por alto cualquier columna que determina como no interesante.  
  
#### <a name="maximumoutputattributes"></a>MAXIMUM_OUTPUT_ATTRIBUTES  
 De forma similar, si un modelo contiene más columnas de predicción que el número especificado en el parámetro *MAXIMUM_OUTPUT_ATTRIBUTES* , el algoritmo pasa por alto cualquier columna que determina como no interesante.  
  
#### <a name="maximumstates"></a>MAXIMUM_STATES  
 Si un modelo contiene más casos de los especificados en el parámetro *MAXIMUM_STATES* , los estados con menor popularidad se agrupan y se tratan como estados que faltan. Si alguno de estos parámetros se establece en 0, la selección de características se desactiva. Esto afecta al tiempo de procesamiento y al rendimiento.  
  
 Además de estos métodos para la selección de características, es posible mejorar la capacidad del algoritmo para identificar o promover atributos significativos estableciendo *marcas de modelado* en el modelo o *marcas de distribución* en la estructura. Para más información sobre estos conceptos, vea [Marcas de modelado &#40;minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md) y [Distribuciones de columnas &#40;minería de datos&#41;](../../analysis-services/data-mining/column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Personalizar la estructura y los modelos de minería de datos](../../analysis-services/data-mining/customize-mining-models-and-structure.md)  
  
  
