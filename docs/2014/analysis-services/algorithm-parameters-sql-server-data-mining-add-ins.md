---
title: Parámetros de algoritmo (datos de SQL Server a los complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_STATES
- FORCED_REGRESSOR
- PERIODICITY_HINT
- HOLDOUT_SEED
- MAXIMUM_ITEMSET_SIZE
- HIDDEN_NODE_RATIO
- CLUSTERING_METHOD
- FORECAST_METHOD
- STOPPING_TOLERANCE
- MISSING_VALUE_SUBSTITUTION
- MINIMUM_IMPORTANCE
- HISTORIC_MODEL_COUNT
- SPLIT_METHOD
- MAXIMUM_OUTPUT_ATTRIBUTES
- HOLDOUT_PERCENTAGE
- MINIMUM_PROBABILITY
- SAMPLE_SIZE
- HISTORICAL_MODEL_GAP
- CLUSTER_SEED
- SCORE_METHOD
- INSTABILITY_SENSITIVITY
- AUTO_DETECT_PERIODICITY
- MAXIMUM_SEQUENCE_STATES
- MINIMUM_DEPENDENCY_PROBABILITY
- MINIMUM_SUPPORT
- MAXIMUM_SUPPORT
- MINIMUM_ITEMSET_SIZE
- PREDICTION_SMOOTHING
- algorithm parameters
- MAXIMUM_SERIES_VALUE
- MODELLING_CARDINALITY
- MAXIMUM_INPUT_ATTRIBUTES
- MINIMUM_SERIES_VALUE
- MAXIMUM_ITEMSET_COUNT
- CLUSTER_COUNT
- COMPLEXITY_PENALTY
ms.assetid: fcdc3f85-813d-4279-90b0-16e26edd008d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92ff53ae795fa4d0565ca9b1537a7d12bc8f0b5b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147615"
---
# <a name="algorithm-parameters-sql-server-data-mining-add-ins"></a>Parámetros de algoritmo (Complementos de minería de datos de SQL Server)
  Cuando se realiza la minería de datos con las Herramientas de análisis de tabla para Excel, no es necesario configurar el algoritmo de minería de datos ni ningún parámetro; cada herramienta analiza los datos y selecciona automáticamente los parámetros óptimos. Sin embargo, si desea modificar el modelo o crear un modelo de minería de datos desde cero, el Cliente de minería de datos para Excel dispone de varias opciones para la personalización.  
  
-   Crear un modelo de minería de datos manualmente, haga clic en **avanzadas** y, a continuación, haga clic en **Agregar modelo a estructura**.  
  
-   Utilice cualquiera de los asistentes de modelado en el cliente de minería de datos y haga clic en **parámetros** para controlar el comportamiento de la [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de minería de datos.  
  
-   Haga clic en **consulta** para abrir el Asistente para modelo de consulta y, a continuación, haga clic en **avanzadas** para abrir el **Editor minería de datos avanzada consulta**. En este editor, puede generar modelos usando plantillas DMX.  
  
 También puede modificar el comportamiento de los modelos de minería de datos ya creados o filtrar los resultados estableciendo parámetros en el visor de modelos de minería de datos.  
  
## <a name="list-of-algorithm-parameters"></a>Lista de parámetros de algoritmo  
 Todos los algoritmos de [!INCLUDE[msCoName](../includes/msconame-md.md)] se pueden personalizar mediante el establecimiento de parámetros. Dado que la mejor configuración de los parámetros depende de la composición de los datos, una explicación completa de los efectos del cambio de parámetros queda fuera del ámbito de este tema.  
  
 En la tabla siguiente hallará una lista de los parámetros, una descripción de su funcionalidad y vínculos a información más técnica.  
  
|Nombre del parámetro|Se usa en|Descripción|  
|--------------------|-------------|-----------------|  
|AUTO_DETECT_PERIODICITY|Algoritmo de serie temporal de Microsoft|Especifica un valor numérico entre 0 y 1 que se usa para detectar la periodicidad. Cuando este valor es más cercano a 1 se favorece el descubrimiento de varios patrones casi periódicos y la generación automática de sugerencias de periodicidad. Un gran número de sugerencias de periodicidad puede aumentar el tiempo de entrenamiento de los modelos y proporcionar modelos más precisos. Si el valor está más próximo a 0, la periodicidad sólo se detecta en datos con una periodicidad muy marcada.<br /><br /> El valor predeterminado es 0,6.|  
|CLUSTER_COUNT|Algoritmo de clústeres de Microsoft<br /><br /> Algoritmo de clústeres de secuencia de Microsoft|Especifica el número aproximado de clústeres que generará el algoritmo. Si no se puede generar el número aproximado de clústeres a partir de los datos, el algoritmo genera tantos clústeres como sea posible. Si CLUSTER_COUNT se establece en 0, el algoritmo utiliza la heurística para determinar el mejor número de clústeres que debe generar.<br /><br /> El valor predeterminado es 10.|  
|CLUSTER_SEED|Algoritmo de clústeres de Microsoft|Especifica el número de inicialización usado para generar clústeres aleatoriamente para la fase inicial de generación del modelo.<br /><br /> El valor predeterminado es 0.|  
|CLUSTERING_METHOD|Algoritmo de clústeres de Microsoft|Especifica el método de agrupación en clústeres que va a usar el algoritmo. Los métodos de agrupación en clústeres disponibles son: EM escalable (1), EM no escalable (2), mediana-K escalable (3) y mediana-K no escalable (4).<br /><br /> El valor predeterminado es 1.|  
|COMPLEXITY_PENALTY|Algoritmo de árboles de decisión de Microsoft<br /><br /> Algoritmo de serie temporal de Microsoft|Controla el crecimiento del árbol de decisión. Un valor bajo aumenta el número de divisiones y un valor alto lo reduce. El valor predeterminado se basa en el número de atributos de un modelo concreto, como se describe en la lista siguiente:<br /><br /> De 1 a 9 atributos, el valor predeterminado es 0,5.<br /><br /> De 10 a 99 atributos, el valor predeterminado es 0,9.<br /><br /> Para 100 o más atributos, el valor predeterminado es 0,99.<br /><br /> Nota: En los modelos de serie temporal, este parámetro se aplica únicamente a los modelos generados mediante el algoritmo ARTxp, o a modelos mixtos.|  
|FORCED_REGRESSOR|Algoritmo de árboles de decisión de Microsoft<br /><br /> Algoritmo de regresión lineal de Microsoft|Fuerza al algoritmo a usar las columnas indicadas como regresores, independientemente de su importancia según los cálculos del algoritmo.<br /><br /> Nota: Este parámetro sólo se utiliza para árboles de decisión que predicen un atributo continuo. Por definición, un modelo de regresión lineal es un caso especial de árboles de decisión que predice atributos continuos. Sin embargo, cualquier modelo de árbol de decisión puede contener un nodo que representa una fórmula de regresión lineal.|  
|FORECAST_METHOD|Algoritmo de serie temporal de Microsoft|Indica si las predicciones se deben realizar con el algoritmo ARTxp, el algoritmo ARIMA o una combinación de ambos.<br /><br /> El valor predeterminado es MIXED.|  
|HIDDEN_NODE_RATIO|Microsoft Neural Network Algorithm|Especifica la proporción de neuronas ocultas por neuronas de entrada y de salida. La siguiente fórmula determina el número inicial de neuronas de la capa oculta:<br /><br /> HIDDEN_NODE_RATIO * SQRT(Total de neuronas de entrada \* Total de neuronas de salida)<br /><br /> El valor predeterminado es 4,0.|  
|HISTORIC_MODEL_COUNT|Algoritmo de serie temporal de Microsoft|Especifica el número de modelos históricos que se generarán.<br /><br /> El valor predeterminado es 1.|  
|HISTORICAL_MODEL_GAP|Algoritmo de serie temporal de Microsoft|Especifica el intervalo temporal entre dos modelos históricos consecutivos. Por ejemplo, si establece este valor en g, se generarán modelos históricos para datos truncados por segmentos temporales a intervalos de g, 2*g, 3\*g, etc.<br /><br /> El valor predeterminado es 10.|  
|HOLDOUT_PERCENTAGE|Algoritmo de regresión logística de Microsoft<br /><br /> Microsoft Neural Network Algorithm|Especifica el porcentaje de casos de los datos de entrenamiento que se han usado para calcular el error de datos de exclusión, que se usa como parte de los criterios de detención durante el entrenamiento del modelo de minería de datos.<br /><br /> El valor predeterminado es 30.<br /><br /> Nota: Este parámetro es distinto del valor de porcentaje de datos de exclusión que se aplica a una estructura de minería de datos.|  
|HOLDOUT_SEED|Algoritmo de regresión logística de Microsoft<br /><br /> Microsoft Neural Network Algorithm|Especifica un número que se usa para inicializar el generador pseudoaleatorio cuando el algoritmo determina aleatoriamente los datos de exclusión. Si este parámetro se establece en 0, el algoritmo genera la inicialización basada en el nombre del modelo de minería de datos para garantizar que el contenido del modelo permanece intacto al volver a realizar el proceso.<br /><br /> El valor predeterminado es 0.<br /><br /> Nota: Este parámetro es distinto del valor de inicialización de datos de exclusión que se aplica a una estructura de minería de datos.|  
|INSTABILITY_SENSITIVITY|Algoritmo de serie temporal de Microsoft|Controla el punto en el que la varianza de la predicción supera un cierto umbral y el algoritmo ARTxp suprime las predicciones. El valor predeterminado es 1.<br /><br /> Nota: Este parámetro se aplica solo a modelos mixtos o los modelos que utilizan el algoritmo ARTxp.|  
|MAXIMUM_INPUT_ATTRIBUTES|Algoritmo de clústeres de Microsoft<br /><br /> Algoritmo de árboles de decisión de Microsoft<br /><br /> Algoritmo de regresión lineal de Microsoft<br /><br /> Algoritmo Bayes naive de Microsoft<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Algoritmo de regresión logística de Microsoft|Define el número de atributos de entrada que el algoritmo puede controlar antes de invocar la selección de características. Establezca este valor en 0 para desactivar la selección de características.<br /><br /> El valor predeterminado es 255.|  
|MAXIMUM_ITEMSET_COUNT|Algoritmo de asociación de Microsoft|Especifica el número máximo de conjuntos de elementos que se van a generar. Si no se especifica ningún número, el algoritmo genera todos los conjuntos de elementos posibles.<br /><br /> El valor predeterminado es 200000.|  
|MAXIMUM_ITEMSET_SIZE|Algoritmo de asociación de Microsoft|Especifica el número máximo de elementos que se admiten en un conjunto de elementos. Si este valor se establece en 0, indica que no hay límite para el tamaño del conjunto de elementos.<br /><br /> El valor predeterminado es 3.|  
|MAXIMUM_OUTPUT_ATTRIBUTES|Algoritmo de árboles de decisión de Microsoft<br /><br /> Algoritmo de regresión lineal de Microsoft<br /><br /> Algoritmo de regresión logística de Microsoft<br /><br /> Algoritmo Bayes naive de Microsoft<br /><br /> Microsoft Neural Network Algorithm|Define el número de atributos de salida que el algoritmo puede controlar antes de invocar la selección de características. Establezca este valor en 0 para desactivar la selección de características.<br /><br /> El valor predeterminado es 255.|  
|MAXIMUM_SEQUENCE_STATES|Algoritmo de clústeres de secuencia de Microsoft|Especifica el número máximo de estados que puede tener una secuencia. Si se establece este valor en un número mayor que 100, el algoritmo puede crear un modelo que no proporcione información significativa.<br /><br /> El valor predeterminado es 64.|  
|MAXIMUM_SERIES_VALUE|Algoritmo de serie temporal de Microsoft|Especifica el valor máximo que se debe usar para las predicciones. Este parámetro se usa, junto con MINIMUM_SERIES_VALUE, para restringir las predicciones a un intervalo esperado. Por ejemplo, puede especificar que la predicción de la cantidad de ventas diaria nunca supere el número de productos en inventario.|  
|MAXIMUM_STATES|Algoritmo de clústeres de Microsoft<br /><br /> Microsoft Neural Network Algorithm<br /><br /> Algoritmo de clústeres de secuencia de Microsoft|Especifica el número máximo de estados de atributo que admite el algoritmo. Si el número de estados de un atributo es mayor que el número máximo de estados, el algoritmo usará los estados más frecuentes del atributo y omitirá los estados restantes.<br /><br /> El valor predeterminado es 100.|  
|MAXIMUM_SUPPORT|Algoritmo de asociación de Microsoft|Especifica el número máximo de casos en los que un conjunto de elementos puede tener soporte. Si este valor es menor que 1, el valor representa un porcentaje del total de casos. Si este valor es mayor que 1, el valor representa el número absoluto de casos que pueden contener el conjunto de elementos.<br /><br /> El valor predeterminado es 1.|  
|MINIMUM_IMPORTANCE|Algoritmo de asociación de Microsoft|Especifica el umbral de importancia para las reglas de asociación. Las reglas con una importancia menor que este valor son filtradas.|  
|MINIMUM_ITEMSET_SIZE|Algoritmo de asociación de Microsoft|Especifica el número mínimo de elementos que se admiten en un conjunto de elementos.<br /><br /> El valor predeterminado es 1.|  
|MINIMUM_DEPENDENCY_PROBABILITY|Algoritmo Bayes naive de Microsoft|Especifica la probabilidad de dependencia mínima entre los atributos de entrada y salida. Este valor se utiliza para limitar el tamaño del contenido generado por el algoritmo. El valor de esta propiedad puede establecerse en un valor comprendido entre 0 y 1. Los valores mayores reducen el número de atributos en el contenido del modelo.<br /><br /> El valor predeterminado es 0,5.|  
|MINIMUM_PROBABILITY|Algoritmo de asociación de Microsoft|Especifica la probabilidad mínima de que se cumpla una regla. Por ejemplo, si este valor se establece en 0,5, especifica que no se generará ninguna regla con menos del cincuenta por ciento de probabilidad.<br /><br /> El valor predeterminado es 0.4.|  
|MINIMUM_SERIES_VALUE|Algoritmo de serie temporal de Microsoft|Especifica la restricción más baja para cualquier predicción de serie temporal. Los valores de predicción nunca serán menores que esta restricción.|  
|MINIMUM_SUPPORT|Algoritmo de asociación de Microsoft|Especifica el número mínimo de casos que debe contener el conjunto de elementos antes de que el algoritmo genere una regla. Si se establece un valor inferior a 1, se especifica el número mínimo de casos como un porcentaje de los casos totales. Si se establece un número entero mayor que 1, se especifica el número mínimo de casos como el número absoluto de casos que debe contener el conjunto de elementos. Si la memoria es limitada, el algoritmo puede incrementar el valor de este parámetro.<br /><br /> El valor predeterminado es 0.03.|  
|MINIMUM_SUPPORT|Algoritmo de clústeres de Microsoft|Especifica el número mínimo de casos de cada clúster.<br /><br /> El valor predeterminado es 1.|  
|MINIMUM_SUPPORT|Algoritmo de árboles de decisión de Microsoft|Determina el número mínimo de casos de hoja necesarios para generar una división en el árbol de decisión.<br /><br /> El valor predeterminado es 10.|  
|MINIMUM_SUPPORT|Algoritmo de clústeres de secuencia de Microsoft|Especifica el número mínimo de casos de cada clúster.<br /><br /> El valor predeterminado es 10.|  
|MINIMUM_SUPPORT|Algoritmo de serie temporal de Microsoft|Especifica el número mínimo de segmentos de tiempo necesarios para generar una división en cada árbol de serie temporal.<br /><br /> El valor predeterminado es 10.|  
|MISSING_VALUE_SUBSTITUTION|Algoritmo de serie temporal de Microsoft|Especifica el método usado para rellenar los espacios en los datos históricos. De forma predeterminada, no se admiten los espacios o bordes irregulares en los datos. Los métodos siguientes se pueden utilizar para rellenar espacios o bordes irregulares: usar el valor anterior, usar el valor promedio o usar una constante numérica concreta.|  
|MODELLING_CARDINALITY|Algoritmo de clústeres de Microsoft|Especifica el número de modelos de ejemplo que se generan durante el proceso de agrupación en clústeres.<br /><br /> El valor predeterminado es 10.|  
|PERIODICITY_HINT|Algoritmo de serie temporal de Microsoft|Proporciona una sugerencia al algoritmo en cuanto a la periodicidad de los datos. Por ejemplo, si las ventas varían por año y la unidad de medida en la serie son los meses, la periodicidad es 12. Este parámetro toma el formato de {n [, n]}, donde n es un número positivo. La n entre corchetes [] es opcional y puede repetirse con la frecuencia que sea necesaria.<br /><br /> De manera predeterminada, es {1}.|  
|PREDICTION_SMOOTHING|Algoritmo de serie temporal de Microsoft|Controla la mezcla de algoritmos de serie temporal ARTXP y ARIMA. El valor especificado sólo es válido cuando el parámetro FORECAST_METHOD está establecido en MIXED. Los valores deben estar entre 0 y 1. Si el valor es 0, el modelo sólo usa ARTXP. Si el valor es 1, el modelo sólo usa ARIMA. Un valor más cercano a 0 concede más importancia a ARTXP. Un valor más cercano a 1 concede más importancia a ARIMA.|  
|SAMPLE_SIZE|Algoritmo de clústeres de Microsoft|Especifica el número de casos que usa el algoritmo en cada paso si el parámetro CLUSTERING_METHOD está establecido en uno de los métodos de agrupación en clústeres escalables. Si establece el parámetro SAMPLE_SIZE en 0, todo el conjunto de datos se agrupará en un único paso. Esto puede causar problemas de memoria y de rendimiento.<br /><br /> El valor predeterminado es 50000.|  
|SAMPLE_SIZE|Algoritmo de regresión logística de Microsoft<br /><br /> Microsoft Neural Network Algorithm|Especifica el número de casos que se van a usar para realizar el entrenamiento del modelo. El proveedor de algoritmos usa el valor menor entre este número o el porcentaje del total de los casos que no están incluidos en el porcentaje de datos de exclusión según se especifica en el parámetro HOLDOUT_PERCENTAGE.<br /><br /> En otras palabras, si HOLDOUT_PERCENTAGE está establecido en 30, el algoritmo usará el valor de este parámetro o un valor que sea igual al 70 por ciento del número total de casos, el que sea menor.<br /><br /> El valor predeterminado es 10000.|  
|SCORE_METHOD|Algoritmo de árboles de decisión de Microsoft|Determina el método usado para calcular el resultado de la división. Las opciones disponibles son: (1) Entropía, (2) Bayesiano con prioridad K2 o (3) Equivalente Dirichlet bayesiano con prioridad uniforme (BDE).<br /><br /> El valor predeterminado es 3.|  
|SPLIT_METHOD|Algoritmo de árboles de decisión de Microsoft|Determina el método usado para dividir el nodo. Las opciones disponibles son: binario (1), completo (2) o ambos (3).<br /><br /> El valor predeterminado es 3.|  
|STOPPING_TOLERANCE|Referencia técnica del algoritmo de clústeres de Microsoft|Especifica el valor que se usa para determinar cuándo se alcanza la convergencia y el algoritmo termina de generar el modelo. La convergencia se alcanza cuando el cambio general de las probabilidades del clúster es inferior al resultado de dividir el parámetro STOPPING_TOLERANCE entre el tamaño del modelo.<br /><br /> El valor predeterminado es 10.|  
  
### <a name="comments"></a>Comentarios  
 Para obtener detalles adicionales sobre los algoritmos, vea los Libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;complementos de minería de datos de SQL Server&#41;](data-mining-algorithms-sql-server-data-mining-add-ins.md)  
  
  
