---
title: Referencia técnica del algoritmo de red neuronal de Microsoft | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- HIDDEN_NODE_RATIO parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- HOLDOUT_PERCENTAGE parameter
- neural network algorithms [Analysis Services]
- output layer [Data Mining]
- neural networks
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- hidden layer
- hidden neurons
- input layer [Data Mining]
- activation function [Data Mining]
- Back-Propagated Delta Rule network
- neural network model [Analysis Services]
- coding [Data Mining]
- HOLDOUT_SEED parameter
ms.assetid: b8fac409-e3c0-4216-b032-364f8ea51095
author: minewiskan
ms.author: owend
ms.openlocfilehash: bf7db49fd2b6a86e9b113dbede785379f910b978
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84521771"
---
# <a name="microsoft-neural-network-algorithm-technical-reference"></a>Referencia técnica del algoritmo de red neuronal de Microsoft
  La red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] usa una red de tipo *perceptrón multinivel* , que también se denomina *red de tipo regla delta de propagación hacia atrás*, compuesta por tres niveles de neuronas o *perceptrones*. Estos niveles son: un nivel de entrada, un nivel oculto opcional y un nivel de salida.  
  
 Esta documentación no abarca una discusión detallada sobre redes neuronales de tipo perceptrón multinivel. En este tema, se explica la implementación básica del algoritmo, incluido el método usado para normalizar los valores de entrada y de salida, y los métodos de selección de características usados para reducir la cardinalidad de los atributos. En este tema, se describen los parámetros y otros valores que se pueden usar para personalizar el comportamiento del algoritmo; además, se proporcionan vínculos a información adicional sobre cómo consultar el modelo.  
  
## <a name="implementation-of-the-microsoft-neural-network-algorithm"></a>Implementación del algoritmo de red neuronal de Microsoft  
 En una red neuronal de tipo perceptrón multinivel, cada neurona recibe una o más entradas y genera una o más salidas idénticas. Cada salida es una función no lineal simple de la suma de las entradas a la neurona. Las entradas pasan de los nodos del nivel de entrada a los nodos del nivel oculto y, a continuación, al nivel de salida; no existe ninguna conexión entre neuronas del mismo nivel. Si no se incluye ningún nivel oculto, tal y como pasa en un modelo de regresión logística, las entradas pasan directamente desde los nodos del nivel de entrada a los nodos del nivel de salida.  
  
 Existen tres tipos de neuronas en una red neuronal creada con el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] :  
  
-   `Input neurons`  
  
 Las neuronas de entrada proporcionan valores de atributo de entrada para el modelo de minería de datos. En el caso de los atributos de entrada discretos, las neuronas de entrada suelen representar un único estado del atributo de entrada. Esto incluye los valores ausentes, si los datos de entrenamiento contienen valores NULL para ese atributo. Un atributo de entrada discreto que tiene más de dos estados genera una neurona de entrada por cada estado y una neurona de entrada para un estado ausente, si existen valores NULL en los datos de entrenamiento. Un atributo de entrada continuo genera dos neuronas de entrada: una neurona para un estado ausente y otra neurona para el valor del propio atributo continuo. Las neuronas de entrada proporcionan entradas para una o más neuronas ocultas.  
  
-   `Hidden neurons`  
  
 Las neuronas ocultas reciben entradas de las neuronas de entrada y proporcionan salidas a las neuronas de salida.  
  
-   `Output neurons`  
  
 Las neuronas de salida representan valores de atributo de predicción para el modelo de minería de datos. En el caso de los atributos de entrada discretos, una neurona de salida suele representar un único estado de predicción para un atributo de predicción, incluidos los valores que faltan. Por ejemplo, un atributo de predicción binario produce un nodo de salida que describe un estado ausente o existente, que indica si existe un valor para ese atributo. Una columna booleana utilizada como un atributo de predicción genera tres neuronas de salida: una neurona para un valor true, otra neurona para un valor false y una última neurona para un estado existente o ausente. Un atributo de predicción discreto que tiene más de dos estados genera una neurona de salida por cada estado y una neurona de salida para un estado ausente o existente. Las columnas de predicción continuas generan dos neuronas de salida: una neurona para  un estado existente o ausente y otra neurona para el valor de la propia columna continua. Si se generan más de 500 neuronas de salida al revisar el conjunto de columnas de predicción, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera una red nueva en el modelo de minería de datos para representar las neuronas de salida adicionales.  
  
 Una neurona recibe la entrada de otras neuronas o de otros datos, dependiendo del nivel de la red en que se encuentra. Una neurona de entrada recibe entradas de los datos originales. Las neuronas ocultas y las neuronas de salida reciben entradas de la salida de otras neuronas de la red neuronal. Las entradas establecen relaciones entre neuronas; estas relaciones sirven como ruta de análisis para un conjunto específico de escenarios.  
  
 Cada entrada tiene un valor asignado denominado *peso*, que describe la relevancia o importancia de dicha entrada en la neurona oculta o en la neurona de salida. Cuanto mayor sea el peso asignado a una entrada, más importante o relevante será el valor de dicha entrada. Los pesos pueden ser negativos, lo cual implica que la entrada puede impedir, en lugar de activar, una neurona específica. El valor de cada entrada se multiplica por el peso para poner de relieve la importancia de la entrada de una neurona específica. En el caso de pesos negativos, el efecto de multiplicar el valor por el peso es una pérdida de importancia.  
  
 Cada neurona tiene una función no lineal sencilla asignada denominada *función de activación*que describe la relevancia o importancia de una neurona específica para ese nivel de una red neuronal. Las neuronas ocultas usan una función *tangente hiperbólica* (tanh) para su función de activación, mientras que las neuronas de salida usan una función *sigmoidea* para la activación. Ambas son funciones no lineales continuas que permiten que la red neuronal modele relaciones no lineales entre neuronas de entrada y salida.  
  
### <a name="training-neural-networks"></a>Redes neuronales de entrenamiento  
 Existen varios pasos implicados en el entrenamiento de un modelo de minería de datos que utiliza el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Estos pasos están muy influenciados por los valores que se especifican en los parámetros de algoritmo.  
  
 En primer lugar, el algoritmo evalúa y extrae los datos de entrenamiento del origen de datos. Un porcentaje de los datos de entrenamiento, denominado *datos de exclusión*, se reserva para evaluar la precisión de la red. Durante el proceso de entrenamiento, la red se evalúa de forma inmediata después de cada iteración mediante los datos de entrenamiento. Cuando la precisión deja de aumentar, el proceso de entrenamiento se detiene.  
  
 Los valores de los parámetros *SAMPLE_SIZE* y *HOLDOUT_PERCENTAGE* se usan para determinar el número de casos de muestra de los datos de aprendizaje y el número de casos que se apartan en los datos de exclusión. El valor del parámetro *HOLDOUT_SEED* se usa para determinar de forma aleatoria los casos individuales que se apartan para los datos de exclusión.  
  
> [!NOTE]  
>  Estos parámetros de algoritmo son diferentes de las propiedades HOLDOUT_SEED y HOLDOUT_SIZE, que se aplican a una estructura de minería de datos para definir un conjunto de datos de prueba.  
  
 A continuación, el algoritmo determina el número y la complejidad de las redes que admite el modelo de minería de datos. Si el modelo contiene uno o más atributos que solamente se utilizan para la predicción, el algoritmo crea una única red que representa todos estos atributos. Si el modelo de minería de datos contiene uno o más atributos que se utilizan para la entrada y la predicción, el proveedor del algoritmo construye una red para cada atributo.  
  
 En el caso de los atributos de entrada y de predicción que tienen valores discretos, cada neurona de entrada o de salida representa respectivamente un único estado. En el caso de los atributos de entrada y de predicción que tienen valores continuos, cada neurona de entrada o de salida representa respectivamente el intervalo y la distribución de valores del atributo. El número máximo de estados admitidos en cada caso depende del valor del parámetro de algoritmo *MAXIMUM_STATES* . Si el número de estados para un atributo específico supera el valor del parámetro de algoritmo *MAXIMUM_STATES* , se eligen los estados más comunes o relevantes para dicho atributo hasta alcanzar el número máximo permitido y el resto de los estados se agrupan como valores ausentes para el análisis.  
  
 Después, el algoritmo usa el valor del parámetro *HIDDEN_NODE_RATIO* al determinar el número inicial de neuronas que se crearán para el nivel oculto. Puede establecer *HIDDEN_NODE_RATIO* en 0 para evitar la creación de un nivel oculto en las redes que genera el algoritmo para el modelo de minería de datos y tratar la red neuronal como una regresión logística.  
  
 El proveedor de algoritmos evalúa iterativamente el peso de todas las entradas de la red simultáneamente, tomando el conjunto de datos de entrenamiento reservado anteriormente y comparando el valor real conocido de cada escenario de los datos de exclusión con la predicción de la red, en un proceso conocido como *aprendizaje por lotes*. Una vez que el algoritmo ha evaluado el conjunto completo de los datos de entrenamiento, revisa el valor predicho y real de cada neurona. El algoritmo calcula el grado de error, si lo hay, y ajusta los pesos asociados con las entradas de esa neurona, trabajando hacia atrás desde las neuronas de salida a las de entrada en un proceso conocido como *propagación hacia atrás*. A continuación, el algoritmo repite el proceso en todo el conjunto de datos de entrenamiento. Dado que el algoritmo puede admitir múltiples pesos y neuronas de salida, el algoritmo de gradiente conjugado se utiliza para guiar el proceso de entrenamiento en la asignación y evaluación de los pesos de las entradas. Esta documentación no abarca una discusión sobre el algoritmo de gradiente conjugado.  
  
### <a name="feature-selection"></a>Selección de características  
 Si el número de atributos de entrada es mayor que el valor del parámetro *MAXIMUM_INPUT_ATTRIBUTES* (o si el número de atributos de predicción es mayor que el valor del parámetro *MAXIMUM_OUTPUT_ATTRIBUTES* ), se usa un algoritmo de selección de características para reducir la complejidad de las redes que se incluyen en el modelo de minería de datos. La selección de características reduce el número de atributos de entrada o de predicción a los más relevantes estadísticamente para el modelo.  
  
 Todos los algoritmos de minería de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usan automáticamente la selección de características para mejorar el análisis y reducir la carga de procesamiento. El método usado para la selección de características en los modelos de red neuronal depende del tipo de datos del atributo. Como referencia, en la tabla siguiente se muestran los métodos de selección de características usados para los modelos de red neuronal; además, se muestran los métodos de selección de características usados para el algoritmo de regresión logística, que está basado en el algoritmo de red neuronal.  
  
|Algoritmo|Método de análisis|Comentarios|  
|---------------|------------------------|--------------|  
|Red neuronal|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|El algoritmo de redes neuronales puede usar ambos métodos de puntuación, el bayesiano y el basado en la entropía, siempre y cuando los datos contengan columnas continuas.<br /><br /> Predeterminada.|  
|Regresión logística|Puntuación interestingness<br /><br /> Entropía de Shannon<br /><br /> Bayesiano con prioridad K2<br /><br /> Dirichlet bayesiano con prioridad uniforme (predeterminado)|Dado que no se puede pasar un parámetro a este algoritmo para controlar el comportamiento de la selección de características, se utilizan los valores predeterminados. Por consiguiente, si todos los atributos son discretos o contienen datos discretos, el valor predeterminado es BDEU.|  
  
 Los parámetros de algoritmo que controlan la selección de características para un modelo de red neuronal son MAXIMUM_INPUT_ATTRIBUTES, MAXIMUM_OUTPUT_ATTRIBUTES y MAXIMUM_STATES. También puede controlar el número de niveles ocultos mediante el establecimiento del parámetro HIDDEN_NODE_RATIO.  
  
### <a name="scoring-methods"></a>Métodos de puntuación  
 La*puntuación* es un tipo de normalización que, en el contexto del entrenamiento de un modelo de red neuronal, hace referencia al proceso de convertir un valor, como una etiqueta de texto discreta, en un valor que se pueda comparar con otros tipos de entradas y que se pueda pesar en la red. Por ejemplo, si un atributo de entrada es Sexo y los valores posibles son Hombre y Mujer, y otro atributo de entrada es Ingresos, con un intervalo de valores variable, los valores para cada atributo no son comparables directamente y, por consiguiente, deben estar codificados a una escala común para que se puedan calcular los pesos. Puntuar es el proceso de normalizar tales entradas para los valores numéricos, específicamente, para un intervalo de probabilidades. Las funciones usadas para la normalización también ayudan a distribuir más uniformemente los valores de entrada en una escala uniforme para que los valores extremos no distorsionen los resultados del análisis.  
  
 Las salidas de la red neuronal también están codificadas. Si hay un único destino para la salida (es decir, la predicción), o varios destinos que se usan solo para la predicción, no para la entrada, el modelo crea una red única y es posible que no sea necesario normalizar los valores. Sin embargo, si se usan varios atributos para la entrada y la predicción, el modelo debe crear varias redes; por tanto, se deben normalizar todos los valores y, al salir de la red, las salidas deberán estar codificadas.  
  
 La codificación de las entradas se basa en la suma de cada valor discreto de los casos de entrenamiento y en la multiplicación de ese valor por su peso. Esto se denomina *suma ponderada*, que se pasa a la función de activación del nivel oculto. Para la codificación, se usa la puntuación-z:  
  
 **Valores discretos**  
  
 μ = p: la probabilidad anterior de un estado  
  
 StdDev = sqrt(p(1-p))  
  
 **Valores continuos**  
  
 Valor presente = 1-μ/σ  
  
 Ningún valor existente =-μ/σ  
  
 Una vez codificados los valores, se realiza una suma ponderada de las entradas, con los extremos de la red como pesos.  
  
 La codificación de las salidas usa la función sigmoidea, que tiene propiedades que la hacen muy útil para la predicción. Una de esas propiedades es que, sin tener en cuenta cómo se ajusta la escala de los valores originales, y sin tener en cuenta si los valores son negativos o positivos, la salida de esta función es siempre un valor entre 0 y 1, lo que resulta apropiado para la estimación de probabilidades. Otra propiedad útil es que la función sigmoidea tiene un efecto suavizador que hace que cuando los valores se alejan del punto de inflexión, la probabilidad del valor se aproxima lentamente a 0 o a 1.  
  
## <a name="customizing-the-neural-network-algorithm"></a>Personalizar el algoritmo de red neuronal  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite varios parámetros que afectan al comportamiento, al rendimiento y a la precisión del modelo de minería de datos resultante. También puede modificar la forma en la que el modelo procesa los datos; para ello, puede establecer marcas de modelado en las columnas o marcas de distribución que especifiquen cómo se deben procesar los valores dentro de la columna.  
  
### <a name="setting-algorithm-parameters"></a>Establecer parámetros del algoritmo  
 En la tabla siguiente, se describen los parámetros que se pueden usar con el algoritmo de red neuronal de Microsoft.  
  
 HIDDEN_NODE_RATIO  
 Especifica la proporción de neuronas ocultas por neuronas de entrada y de salida. La siguiente fórmula determina el número inicial de neuronas de la capa oculta:  
  
 HIDDEN_NODE_RATIO * SQRT(Total de neuronas de entrada \* Total de neuronas de salida)  
  
 El valor predeterminado es 4,0.  
  
 HOLDOUT_PERCENTAGE  
 Especifica el porcentaje de casos de los datos de entrenamiento que se han usado para calcular el error de datos de exclusión, que se usa como parte de los criterios de detención durante el entrenamiento del modelo de minería de datos.  
  
 El valor predeterminado es 30.  
  
 HOLDOUT_SEED  
 Especifica un número que se usa para inicializar el generador pseudoaleatorio cuando el algoritmo determina aleatoriamente los datos de exclusión. Si este parámetro se establece en 0, el algoritmo genera la inicialización basada en el nombre del modelo de minería de datos para garantizar que el contenido del modelo permanece intacto al volver a realizar el proceso.  
  
 El valor predeterminado es 0.  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 Determina el número máximo de atributos de entrada que se pueden proporcionar al algoritmo antes de emplear la selección de características. La función de selección de atributos de entrada se deshabilita cuando este valor se establece en 0.  
  
 El valor predeterminado es 255.  
  
 MAXIMUM_OUTPUT_ATTRIBUTES  
 Determina el número máximo de atributos de salida que se pueden proporcionar al algoritmo antes de emplear la selección de características. La característica de selección de atributos de salida se deshabilita cuando este valor se establece en 0.  
  
 El valor predeterminado es 255.  
  
 MAXIMUM_STATES  
 Especifica el número máximo de estados discretos por atributo que admite el algoritmo. Si en número de estados de un atributo específico es mayor que el número especificado para este parámetro, el algoritmo utiliza los estados más frecuentes de este atributo y trata al resto como estados que faltan.  
  
 El valor predeterminado es 100.  
  
 SAMPLE_SIZE  
 Especifica el número de casos que se van a usar para realizar el entrenamiento del modelo. El algoritmo utiliza el valor menor entre este número o el porcentaje del total de escenarios que no están incluidos en los datos de exclusión, según se especifica en el parámetro HOLDOUT_PERCENTAGE.  
  
 En otras palabras, si HOLDOUT_PERCENTAGE se establece en 30, el algoritmo utilizará el valor de este parámetro o un valor igual al 70 por ciento del número total de casos, según cuál sea menor.  
  
 El valor predeterminado es 10000.  
  
### <a name="modeling-flags"></a>Marcas de modelado  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las siguientes marcas de modelado.  
  
 NOT NULL  
 Indica que la columna no puede contener un valor NULL. Se producirá un error si Analysis Services encuentra un valor NULL durante el entrenamiento del modelo.  
  
 Se aplica a las columnas de la estructura de minería de datos.  
  
 MODEL_EXISTENCE_ONLY  
 Indica que el modelo solo debe considerar si existe un valor para el atributo o si falta un valor. No importa el valor exacto.  
  
 Se aplica a las columnas del modelo de minería de datos.  
  
### <a name="distribution-flags"></a>Marcas de distribución  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las siguientes marcas de distribución. Las marcas solo se usan como sugerencias para el modelo; si el algoritmo detecta una distribución diferente, usará la distribución encontrada, no la proporcionada en la sugerencia.  
  
 Normal  
 Indica que los valores de la columna se deben tratar como si representasen la distribución normal o gaussiana.  
  
 Uniforme  
 Indica que los valores de la columna se deben tratar como si estuviesen distribuidos uniformemente; es decir, la probabilidad de cualquier valor es más o menos la misma y depende del número total de valores.  
  
 Logarítmica normal  
 Indica que los valores de la columna tienen que tratarse como si estuviesen distribuidos según la curva *logarítmica normal* , lo que significa que el logaritmo de los valores se distribuye normalmente.  
  
## <a name="requirements"></a>Requisitos  
 Un modelo de red neuronal debe contener por lo menos una columna de entrada y una columna de salida.  
  
### <a name="input-and-predictable-columns"></a>Columnas de entrada y de predicción  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las columnas de entrada y de predicción específicas que se enumeran en la tabla siguiente.  
  
|Columna|Tipos de contenido|  
|------------|-------------------|  
|Atributo de entrada|Continuous, Cyclical, Discrete, Discretized, Key, Table y Ordered|  
|Atributo de predicción|Continuous, Cyclical, Discrete, Discretized y Ordered|  
  
> [!NOTE]  
>  Se admiten los tipos de contenido Cyclical y Ordered, pero el algoritmo los trata como valores discretos y no realiza un procesamiento especial.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de red neuronal de Microsoft](microsoft-neural-network-algorithm.md)   
 [Contenido del modelo de minería de datos para los modelos de red neuronal &#40;Analysis Services-minería de datos&#41;](mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Ejemplos de consultas de modelos de red neuronal](neural-network-model-query-examples.md)  
  
  
