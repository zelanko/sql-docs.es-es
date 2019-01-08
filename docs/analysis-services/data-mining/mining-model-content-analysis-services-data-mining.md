---
title: Contenido del modelo de minería de datos (Analysis Services - minería de datos) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5fe10a98910f54e4317d0191753d40b9b6b0b94f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52508541"
---
# <a name="mining-model-content-analysis-services---data-mining"></a>Contenido del modelo de minería de datos (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Después de diseñar y procesar un modelo de minería de datos utilizando los datos de la estructura de minería de datos subyacente, el modelo está completo con su *contenido*. Puede utilizar este contenido para realizar predicciones o analizar los datos.  
  
 El contenido del modelo de minería de datos incluye los metadatos sobre el modelo, estadísticas de los datos y los patrones detectados por el algoritmo de minería de datos. Según el algoritmo que se utilizara, el contenido del modelo puede incluir fórmulas de regresión, definiciones de reglas y conjuntos de elementos, o pesos y otras estadísticas.  
  
 Independientemente del algoritmo utilizado, el contenido del modelo de minería de datos se presenta en una estructura estándar. Puede examinar la estructura en el Visor de árbol de contenido genérico de Microsoft, que se proporciona en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y, después, cambiar a uno de los visores personalizados para ver cómo se interpreta y se muestra gráficamente la información para cada tipo de modelo. También puede crear consultas con el contenido del modelo de minería de datos utilizando cualquier cliente que admita el conjunto de filas de esquema MINING_MODEL_CONTENT. Para obtener más información, vea [Tareas y procedimientos de Consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md).  
  
 En esta sección se describe la estructura básica del contenido que se proporciona para todos los tipos de modelos de minería de datos. Describe los tipos de nodos que son comunes a todo el contenido del modelo de minería de datos y proporciona instrucciones para interpretar la información.  
  
 [Estructura del contenido del modelo de minería de datos](#bkmk_Structure)  
  
 [Nodos en el contenido del modelo](#bkmk_Nodes)  
  
 [Contenido del modelo de minería de datos por tipo de algoritmo](#bkmk_AlgoType)  
  
 [Herramientas para ver el contenido del modelo de minería de datos](#bkmk_Viewing)  
  
 [Herramientas para consultar el contenido del modelo de minería de datos](#bkmk_Querying)  
  
##  <a name="bkmk_Structure"></a> Estructura del contenido del modelo de minería de datos  
 El contenido de cada modelo se presenta como una serie de *nodos*. Un nodo es un objeto dentro de un modelo de minería de datos que contiene metadatos e información sobre una parte del mismo. Los nodos están organizados en una jerarquía. La organización exacta de los nodos en la jerarquía y el significado de esta dependen del algoritmo utilizado. Por ejemplo, si crea un modelo de árboles de decisión, puede contener varios árboles, todos conectados a la raíz del modelo; si crea un modelo de red neuronal, el modelo puede contener una o varias redes, además de un nodo de estadísticas.  
  
 El primer nodo de cada modelo se denomina *nodo raíz*o nodo *primario del modelo* . Cada modelo tiene un nodo raíz (NODE_TYPE = 1). El nodo raíz suele contener algunos metadatos sobre el modelo y el número de nodos secundarios, pero poca información adicional sobre los patrones detectados por el modelo.  
  
 Según el algoritmo que se usara para crear el modelo, el nodo raíz tiene un número variable de nodos secundarios. Los nodos segundarios tienen significados diferentes y contenidos distintos, según el algoritmo y la profundidad y complejidad de los datos.  
  
##  <a name="bkmk_Nodes"></a> Nodos en el contenido del modelo de minería de datos  
 En un modelo de minería de datos, un nodo es un contenedor de uso general que almacena una parte de información sobre todo o parte del modelo. La estructura de cada nodo siempre es la misma y contiene las columnas definidas por el conjunto de filas de esquema de minería de datos. Para obtener más información, vea [Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-rowset).  
  
 Cada nodo incluye los metadatos sobre el nodo, incluido un identificador que es único dentro de cada modelo, el identificador del nodo primario y el número de nodos secundarios que tiene el nodo. Los metadatos identifican el modelo al que pertenece el nodo y el catálogo de la base de datos donde ese modelo en particular está almacenado. El contenido adicional que se proporciona en el nodo difiere en función del tipo de algoritmo que se usara para crear el modelo y podría incluir lo siguiente:  
  
-   El recuento de casos en los datos de entrenamiento que admiten un valor de predicción determinado.  
  
-   Estadísticas, como la media, desviación estándar o varianza.  
  
-   Coeficientes y fórmulas.  
  
-   La definición de reglas y punteros laterales.  
  
-   Fragmentos XML que describen una parte del modelo.  
  
### <a name="list-of-mining-content-node-types"></a>Lista de tipos de nodos de contenido de minería de datos  
 En la tabla siguiente se enumeran los diferentes tipos de nodos que se generan en los modelos de minería de datos. Dado que cada algoritmo procesa la información de manera diferente, cada modelo genera solo unos tipos concretos de nodos. Si cambia el algoritmo, el tipo de nodo puede cambiar. Además, si vuelve a procesar el modelo, el contenido de cada nodo puede cambiar.  
  
> [!NOTE]  
>  Si usa un servicio de minería de datos diferente o crear sus propios algoritmos complementarios, tipos de nodos personalizados adicionales pueden estar disponibles.  
  
|NODE_TYPE ID|Etiqueta de nodo|Contenido de nodo|  
|-------------------|----------------|-------------------|  
|1|Modelo|Los metadatos y el nodo de contenido raíz. Se aplica a todos los tipos de modelos.|  
|2|trEE|Nodo raíz de un árbol de clasificación. Se aplica a los modelos del árbol de decisión.|  
|3|Interior|Nodo de división interior en un árbol. Se aplica a los modelos del árbol de decisión.|  
|4|Distribución|Nodo terminal de un árbol. Se aplica a los modelos del árbol de decisión.|  
|5|Clúster|Clúster detectado por el algoritmo. Se aplica a los modelos de agrupación en clústeres y a los modelos de clústeres de secuencia.|  
|6|Desconocido|Tipo de nodo desconocido.|  
|7|ItemSet|Conjunto de elementos detectado por el algoritmo. Se aplica a modelos de asociación o modelos de agrupación en clústeres de secuencia.|  
|8|AssociationRule|Regla de asociación detectada por el algoritmo. Se aplica a modelos de asociación o modelos de agrupación en clústeres de secuencia.|  
|9|PredictableAttribute|Atributo de predicción. Se aplica a todos los tipos de modelos.|  
|10|InputAttribute|Atributo de entrada. Se aplica a los árboles de decisión y los modelos Bayes Naïve.|  
|11|InputAttributeState|Estadísticas sobre los estados de un atributo de entrada. Se aplica a los árboles de decisión y los modelos Bayes Naïve.|  
|13|Secuencia|Nodo superior para un componente del modelo Markov de un clúster de secuencia. Se aplica a los modelos de agrupación en clústeres.|  
|14|Transition|Matriz de transición de Markov. Se aplica a los modelos de agrupación en clústeres.|  
|15|TimeSeries|Nodo no raíz de un árbol de serie temporal. Solo se aplica a los modelos de serie temporal.|  
|16|TsTree|Nodo raíz de un árbol de serie temporal que corresponde a una serie temporal de predicción. Se aplica a los modelos de serie temporal y solo si el modelo se creó utilizando el parámetro MIXED.|  
|17|NNetSubnetwork|Una subred. Se aplica a los modelos de red neuronal.|  
|18|NNetInputLayer|Grupo que contiene los nodos del nivel de entrada. Se aplica a los modelos de red neuronal.|  
|19|NNetHiddenLayer|Grupos que contiene los nodos que describen el nivel oculto. Se aplica a los modelos de red neuronal.|  
|21|NNetOutputLayer|Grupos que contiene los nodos del nivel de salida. Se aplica a los modelos de red neuronal.|  
|21|NNetInputNode|Nodo en el nivel de entrada que coincide un atributo de entrada con los estados correspondientes. Se aplica a los modelos de red neuronal.|  
|22|NNetHiddenNode|Nodo en el nivel oculto. Se aplica a los modelos de red neuronal.|  
|23|NNetOutputNode|Nodo en el nivel de salida. Este nodo normalmente coincidirá con un atributo de salida y los estados correspondientes. Se aplica a los modelos de red neuronal.|  
|24|NNetMarginalNode|Estadísticas marginales sobre el conjunto de entrenamiento. Se aplica a los modelos de red neuronal.|  
|25|RegressionTreeRoot|Raíz de un árbol de regresión. Se aplica a los modelos de regresión lineal y a los modelos de árboles de decisión que contiene atributos de entrada continuos.|  
|26|NaiveBayesMarginalStatNode|Estadísticas marginales sobre el conjunto de entrenamiento. Se aplica a los modelos Bayes Naïve.|  
|27|ArimaRoot|Nodo raíz de un modelo ARIMA. Se aplica solo a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|28|ArimaPeriodicStructure|Estructura periódica en un modelo ARIMA. Se aplica solo a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|29|ArimaAutoRegressive|Coeficiente de regresión automática para un único término en un modelo ARIMA.<br /><br /> Se aplica solo a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|30|ArimaMovingAverage|Coeficiente de la media móvil para un único término en un modelo ARIMA. Se aplica solo a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|1000|CustomBase|Punto inicial para los tipos de nodo personalizados. Los tipos de nodo personalizados deben ser números enteros mayores que esta constante. Se aplica a los modelos creados utilizando algoritmos complementarios personalizados.|  
  
### <a name="node-id-name-caption-and-description"></a>Identificador de nodo, nombre, título y descripción  
 El nodo raíz de cualquier modelo siempre tiene el identificador único 0 (**NODE_UNIQUE_NAME**). Analysis Services asigna automáticamente todos los identificadores de nodo y no se pueden modificar.  
  
 El nodo raíz para cada modelo también contiene algunos metadatos básicos sobre el modelo. Estos metadatos incluyen la base de datos de Analysis Services donde el modelo está almacenado (**MODEL_CATALOG**), el esquema (**MODEL_SCHEMA**) y el nombre del modelo (**MODEL_NAME**). Sin embargo, esta información se repite en todos los nodos del modelo, de modo que no necesita consultar el nodo raíz para obtener estos metadatos.  
  
 Además de un nombre usado como identificador único, cada nodo tiene un *nombre* (**NODE_NAME**). Este nombre lo crea automáticamente el algoritmo para la presentación y no se puede modificar.  
  
> [!NOTE]  
>  El algoritmo de clústeres de Microsoft permite a los usuarios asignar nombres descriptivos a cada clúster. Sin embargo, estos nombres descriptivos no se conservan en el servidor y, si vuelve a procesar el modelo, el algoritmo generará nombres de clúster nuevos.  
  
 El algoritmo genera automáticamente el *título* y la *descripción* para cada nodo, que actúan como etiquetas para ayudarle a entender el contenido del nodo. El texto generado para cada campo depende del tipo de modelo. En algunos casos, el nombre, el título y la descripción pueden contener exactamente la misma cadena, pero, en algunos modelos, la descripción puede contener información adicional. Consulte el tema sobre el tipo de modelo individual para obtener detalles de la implementación.  
  
> [!NOTE]  
>  El servidor de Analysis Services solo admite el cambio de nombre de los nodos si los modelos se generan utilizando un algoritmo complementario personalizado que implemente el cambio de nombre. Para habilitar el cambio de nombre, debe invalidar los métodos al crear el algoritmo complementario.  
  
### <a name="node-parents-node-children-and-node-cardinality"></a>Nodo primarios, nodos secundarios y cardinalidad de los nodos  
 La relación entre los nodos primarios y los nodos secundarios en una estructura de árbol se determina mediante el valor de la columna PARENT_UNIQUE_NAME. Este valor está almacenado en el nodo secundario y le indica el identificador del nodo primario. A continuación se proporcionan algunos ejemplos de cómo se podría utilizar esta información:  
  
-   Una columna PARENT_UNIQUE_NAME que sea NULL significa que el nodo es el nodo superior del modelo.  
  
-   Si el valor de PARENT_UNIQUE_NAME es 0, el nodo debe ser un descendiente directo del nodo superior en el modelo. Esto se debe a que el identificador del nodo raíz es 0 siempre.  
  
-   Puede utilizar funciones dentro de una consulta de Extensiones de minería de datos (DMX) para encontrar los descendientes o los elementos primarios de un nodo determinado. Para obtener más información sobre cómo usar funciones en las consultas, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
 La*cardinalidad* hace referencia al número de elementos en un conjunto. En el contexto de un modelo de minería de datos procesado, la cardinalidad indica el número de elementos secundarios de un nodo determinado. Por ejemplo, si un modelo de árbol de decisión tuviera un nodo para [Ingresos anuales] y ese nodo tuviera dos nodos secundarios, uno para la condición [Ingresos anuales] = Altos y otro para la condición [Ingresos anuales] = Bajos, el valor de CHILDREN_CARDINALITY para el nodo [Ingresos anuales] sería 2.  
  
> [!NOTE]  
>  En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], únicamente los nodos secundarios inmediatos se cuentan al calcular la cardinalidad de un nodo. Sin embargo, si crea un algoritmo complementario personalizado, puede sobrecargar CHILDREN_CARDINALITY para contar la cardinalidad de manera diferente. Por ejemplo, esto puede ser útil si deseara contabilizar el número total de descendientes, no simplemente los elementos secundarios inmediatos.  
  
 Aunque la cardinalidad se contabiliza de la misma manera para todos los modelos, la forma en que se interpreta o usa el valor de la cardinalidad difiere según el tipo del modelo. Por ejemplo, en un modelo de agrupación en clústeres, la cardinalidad del nodo superior indica el número total de clústeres que se encontraron. En otros tipos de modelos, la cardinalidad puede tener siempre un valor establecido que depende del tipo de nodo. Para obtener más información sobre cómo interpretar la cardinalidad, vea el tema sobre el tipo de modelo individual.  
  
> [!NOTE]  
>  Algunos modelos, como los creados por el algoritmo de red neuronal de Microsoft, contienen además un tipo de nodo especial que proporciona estadísticas descriptivas sobre los datos de entrenamiento para el modelo completo. Por definición, estos nodos nunca tienen nodos secundarios.  
  
### <a name="node-distribution"></a>distribución de nodos  
 La columna NODE_DISTRIBUTION contiene una tabla anidada que en muchos nodos proporciona información importante y detallada sobre los modelos que detecta el algoritmo. Las estadísticas exactas que se proporcionan en esta tabla cambian según el tipo de modelo, la posición del nodo en el árbol y si el atributo de predicción es un valor numérico continuo o discreto; sin embargo, pueden incluir los valores mínimo y máximo de un atributo, los pesos asignados a los valores, el número de casos de un nodo, los coeficientes que se usan en una fórmula de regresión y medidas estadísticas como la desviación estándar y la varianza. Para obtener más información sobre cómo interpretar la distribución de los nodos, consulte el tema correspondiente al tipo específico de modelo con el que está trabajando.  
  
> [!NOTE]  
>  La tabla NODE_DISTRIBUTION puede estar vacía, dependiendo del tipo de nodo. Por ejemplo, algunos nodos solo sirven para organizar una colección de nodos secundarios y son estos los que contienen las estadísticas detalladas.  
  
 La tabla anidada, NODE_DISTRIBUTION, siempre contiene las columnas siguientes. El contenido de cada columna varía según el tipo del modelo. Para obtener más información sobre tipos de modelo concretos, vea [Contenido del modelo de minería de datos por tipo de algoritmo](#bkmk_AlgoType).  
  
 ATTRIBUTE_NAME  
 El contenido varía según el algoritmo. Puede ser el nombre de una columna, como un atributo de predicción, una regla, un conjunto de elementos o un fragmento de información interno al algoritmo, como parte de una fórmula.  
  
 Esta columna también puede contener un par atributo-valor.  
  
 ATTRIBUTE_VALUE  
 Valor del atributo denominado en ATTRIBUTE_NAME.  
  
 Si el nombre de atributo es una columna, en el caso más sencillo, ATTRIBUTE_VALUE contiene uno de los valores discretos para esa columna.  
  
 En función de cómo el algoritmo procese los valores, ATTRIBUTE_VALUE también puede contener una marca que indique si existe un valor para el atributo (**Existing**) o si el valor es nulo (**Missing**).  
  
 Por ejemplo, si un modelo se configura para encontrar los clientes que han comprado por lo menos una vez un elemento determinado, la columna ATTRIBUTE_NAME podría contener el par atributo-valor que define el elemento de interés, como `Model = 'Water bottle'`, y la columna ATTRIBUTE_VALUE contendría únicamente la palabra clave **Existing** o **Missing**.  
  
 Support  
 Recuento de los casos que tienen este par atributo-valor o que contienen este conjunto de elementos o regla.  
  
 En general, para cada nodo, el valor de compatibilidad indica cuántos casos en el conjunto de entrenamiento están incluidos en el nodo actual. En la mayor parte de los tipos de modelo, la compatibilidad representa un recuento exacto de casos. Los valores de compatibilidad son útiles porque se puede ver la distribución de los datos dentro de los casos de entrenamiento sin tener que consultar los datos de entrenamiento. El servidor de Analysis Services también utiliza estos valores almacenados para calcular la probabilidad almacenada con respecto a la probabilidad anterior, a fin de determinar si la inferencia es fuerte o débil.  
  
 Por ejemplo, en un árbol de clasificación, el valor de compatibilidad indica el número de casos que tienen la combinación descrita de atributos.  
  
 En un árbol de decisión, la suma de compatibilidad en cada nivel de un árbol suma la compatibilidad de su nodo primario. Por ejemplo, si un modelo que contiene 1200 casos se divide igualmente por género y, a continuación, se subdivide igualmente por tres valores para los nodos de ingresos bajo, medio y alto, el elemento secundario del nodo (2), que son nodos (4), (5) y (6), siempre suman el mismo número de casos como nodo (2).  
  
|Identificador de nodo y atributos de nodo|Recuento de soporte|  
|---------------------------------|-------------------|  
|(1) Raíz del modelo|1200|  
|(2) Género = Varón<br /><br /> (3) Género = Mujer|600<br /><br /> 600|  
|(4) Género = Varón e Ingresos = Altos<br /><br /> (5) Género = Varón e Ingresos = Medios<br /><br /> (6) Género = Varón e Ingresos = Bajos|200<br /><br /> 200<br /><br /> 200|  
|(7) Género = Mujer e Ingresos = Altos<br /><br /> (8) Género = Mujer e Ingresos = Medios<br /><br /> (9) Género = Mujer e Ingresos = Bajos|200<br /><br /> 200<br /><br /> 200|  
  
 En un modelo de agrupación en clústeres, la cifra correspondiente a la compatibilidad se puede ponderar para incluir las probabilidades de pertenecer a varios clústeres. La pertenencia a varios clústeres es el método de agrupación en clústeres predeterminado. En este escenario, dado que cada caso no pertenece necesariamente a un clúster y solo a uno, la compatibilidad en estos modelos podría no sumar el 100 por ciento a través de todos los clústeres.  
  
 PROBABILITY  
 Indica la probabilidad para este nodo concreto dentro del modelo completo.  
  
 Generalmente, la probabilidad representa la compatibilidad para este valor determinado, dividido por el recuento total de casos dentro del nodo (NODE_SUPPORT).  
  
 Sin embargo, la probabilidad se ajusta ligeramente para eliminar la desviación producida por los valores que están ausentes en los datos.  
  
 Por ejemplo, si los valores actuales para [Elementos secundarios totales] es 'Uno' y 'Dos', es aconsejable evitar crear un modelo que prediga que es imposible no tener ningún elemento secundario o tener tres. Para asegurarse de que los valores ausentes son improbables, pero no imposibles, el algoritmo suma siempre 1 al recuento de valores reales para cualquier atributo.  
  
 Ejemplo:  
  
 Probabilidad de [Elementos secundarios totales = Uno] = [Recuento de casos donde elementos secundarios totales = Uno] +1/[Recuento de todos los casos] +3  
  
 Probabilidad de [Elementos secundarios totales = Dos] = [Recuento de casos donde elementos secundarios totales = Dos] +1/[Recuento de todos los casos] +3  
  
> [!NOTE]  
>  El ajuste de 3 se calcula sumando 1 al número total de valores existentes, n.  
  
 Después del ajuste, las probabilidades de todos los valores suman todavía 1. La probabilidad para el valor sin datos (en este ejemplo, [Elementos secundarios totales = 'Cero', 'Tres' o algún otro valor]), se inicia en un nivel distinto de cero muy bajo y sube despacio cuando se agregan más casos.  
  
 varianza  
 Indica la varianza de los valores dentro del nodo. Por definición, la varianza siempre es 0 para los valores discretos. Si el modelo admite valores continuos, la varianza se calcula como σ (sigma), usando el denominador n o el número de casos en el nodo.  
  
 En general se usan dos definiciones para representar la desviación estándar (**StDev**). Un método para calcular la desviación estándar tiene en cuenta la desviación de la cuenta y otro método calcula la desviación estándar sin utilizar la desviación. En general, los algoritmos de minería de datos de Microsoft no utilizan la desviación al calcular la desviación estándar.  
  
 El valor que aparece en la tabla NODE_DISTRIBUTION es el valor real para todos los atributos discretos y de datos discretos, y la media para los valores continuos.  
  
 VALUE_TYPE  
 Indica el tipo de datos del valor o un atributo, y el uso del valor. Ciertos tipos de valores solo se aplican a ciertos tipos de modelos:  
  
|VALUE_TYPE ID|Etiqueta del valor|Nombre del tipo de valor|  
|--------------------|-----------------|---------------------|  
|1|Missing|Indica que los datos del caso no contenían un valor para este atributo. El estado **Missing** se calcula de forma independiente de los atributos que tienen valores.|  
|2|Existing|Indica que los datos del caso contienen un valor para este atributo.|  
|3|Continuous|Indica que el valor del atributo es un valor numérico continuo y, por consiguiente, puede ser representado por una media, junto con la varianza y la desviación estándar.|  
|4|Discrete|Indica un valor, numérico o de texto, que se trata como discreto.<br /><br /> **Nota** Los valores discretos también pueden ser ausentes; sin embargo, se tratan de forma diferente al realizar cálculos. Para obtener información, vea [Valores ausentes &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/missing-values-analysis-services-data-mining.md).|  
|5|Discretized|Indica que el atributo contiene valores numéricos que se han convertido en datos discretos. El valor será una cadena con formato que describe los depósitos de discretización.|  
|6|Existing|Indica que el atributo tiene valores numéricos continuos y que los valores se han proporcionado en los datos, frente a los valores que están ausentes o se han deducido.|  
|7|Coeficiente|Indica un valor numérico que representa un coeficiente.<br /><br /> Un coeficiente es un valor que se aplica al calcular el valor de la variable dependiente. Por ejemplo, si un modelo crea una fórmula de regresión que predice los ingresos según la edad, el coeficiente se utiliza en la fórmula que relaciona la edad con los ingresos.|  
|8|Ganancia de puntuación|Indica un valor numérico que representa la ganancia de puntuación para un atributo.|  
|9|Estadísticas|Indica un valor numérico que representa una estadística para un regresor.|  
|10|Nombre de nodo exclusivo|Indica que el valor no se debería tratar como numérico o cadena, sino como el identificador único de otro nodo de contenido en un modelo.<br /><br /> Por ejemplo, en un modelo de red neuronal, los identificadores proporcionan punteros de los nodos del nivel de salida a los nodos del nivel oculto y de los nodos del nivel oculto a los nodos del nivel de salida.|  
|11|Interceptar|Indica un valor numérico que representa la intersección en una fórmula de regresión.|  
|12|Periodicidad|Indica que el valor denota una estructura periódica en un modelo.<br /><br /> Solo se aplica a los modelos de serie temporal que contienen un modelo ARIMA.<br /><br /> Nota: El algoritmo de serie temporal de Microsoft detecta automáticamente estructuras periódicas según los datos de entrenamiento. Como resultado, las periodicidades en el modelo final pueden incluir valores de periodicidad que no se proporcionaron como parámetro al crear el modelo.|  
|13|Orden de regresión automática|Indica que el valor representa el número de serie de regresión automática.<br /><br /> Se aplica a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|14|Orden de media móvil|Representa el número de medias móviles en una serie.<br /><br /> Se aplica a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|15|Orden de diferencia|Indica que el valor muestra cuántas veces se diferencia la serie.<br /><br /> Se aplica a los modelos de serie temporal que utilizan el algoritmo ARIMA.|  
|16|Boolean|Representa un tipo booleano.|  
|17|Otros|Representa un valor personalizado definido por el algoritmo.|  
|18|Cadena representada|Representa un valor personalizado que el algoritmo representa como una cadena. El modelo de objetos no aplicó ningún formato.|  
  
 Los tipos de valores se derivan de la enumeración ADMOMD.NET. Para obtener más información, vea <xref:Microsoft.AnalysisServices.AdomdServer.MiningValueType>.  
  
### <a name="node-score"></a>Puntuación del nodo  
 El significado de la puntuación del nodo difiere en función del tipo de modelo y también puede ser específico del tipo de nodo. Para obtener información sobre cómo se calcula NODE_SCORE para cada modelo y tipo de nodo, vea [Contenido del modelo de minería de datos por tipo de algoritmo](#bkmk_AlgoType).  
  
### <a name="node-probability-and-marginal-probability"></a>Probabilidad de nodo y probabilidad marginal  
 El conjunto de filas de esquema de modelos de minería de datos incluye las columnas NODE_PROBABILITY y MARGINAL_PROBABILITY para todos los tipos de modelos. Estas columnas solo contienen valores en los nodos en los que un valor de probabilidad es significativo. Por ejemplo, el nodo raíz de un modelo nunca contiene una puntuación de probabilidad.  
  
 En aquellos nodos que proporcionan puntuaciones de probabilidad, la probabilidad de nodo y las probabilidades marginales representan cálculos diferentes.  
  
-   **La probabilidad marginal** es la probabilidad de alcanzar el nodo a partir de su elemento primario.  
  
-   **La probabilidad de nodo** es la probabilidad de alcanzar el nodo desde la raíz.  
  
-   **La probabilidad de nodo** siempre es mayor o igual que **la probabilidad marginal**.  
  
 Por ejemplo, si la población de todos los clientes en un árbol de decisión está dividida por igual por el género (y no falta ningún valor), la probabilidad de los nodos secundarios debería ser 5. Sin embargo, suponga que cada uno de los nodos correspondientes al género se divide por igual por niveles de ingresos-altos, medios y bajos. En este caso, la puntuación MARGINAL_PROBABILITY de cada nodo secundario siempre debería ser 0,33, pero el valor NODE_PROBABILTY será el producto de todas las probabilidades que conducen a ese nodo y, por tanto, siempre será menor que el valor de MARGINAL_PROBABILITY.  
  
|Nivel de nodo/atributo y valor|La probabilidad marginal|La probabilidad de nodo|  
|----------------------------------------|--------------------------|----------------------|  
|Raíz del modelo<br /><br /> Todos los clientes de destino|1|1|  
|Los clientes de destino divididos por género|.5|.5|  
|Los clientes de destino divididos por género y divididos de nuevo de tres maneras por ingresos|.33|.5 * .33 = .165|  
  
### <a name="node-rule-and-marginal-rule"></a>Regla de nodo y regla marginal  
 El conjunto de filas de esquema de modelos de minería de datos también incluye las columnas NODE_RULE y MARGINAL_RULE para todos los tipos de modelos. Estas columnas contienen fragmentos XML que se pueden utilizar para serializar un modelo o para representar alguna parte de la estructura del modelo. Estas columnas pueden estar en blanco para algunos nodos, si un valor careciera de sentido.  
  
 Se proporcionan dos tipos de reglas XML, similares a los dos tipos de valores de probabilidad. El fragmento XML en MARGINAL_RULE define el atributo y el valor para el nodo actual, mientras que el fragmento XML en NODE_RULE describe la ruta de acceso al nodo actual desde la raíz del modelo.  
  
##  <a name="bkmk_AlgoType"></a> Contenido del modelo de minería de datos por tipo de algoritmo  
 Cada algoritmo almacena tipos diferentes de información como parte de su esquema de contenido. Por ejemplo, el algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] genera muchos nodos secundarios, cada uno de los cuales representa un posible clúster. Cada nodo de clúster contiene las reglas que describen las características que comparten los elementos en el clúster. Por el contrario, el algoritmo de regresión lineal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] no contiene ningún nodo secundario; en su lugar, el nodo primario para el modelo contiene la ecuación que describe la relación lineal detectada mediante el análisis.  
  
 En la tabla siguiente se proporcionan vínculos a temas correspondientes a cada tipo de algoritmo.  
  
-   **Temas de contenido del modelo:** Explica el significado de cada tipo de nodo para cada tipo de algoritmo y proporcionan orientación sobre qué nodos son de más interés en un tipo de modelo determinado.  
  
-   **Temas de consulta:** Se proporcionan ejemplos de consultas de un tipo de modelo determinado y orientación sobre cómo interpretar los resultados.  
  
|Algoritmo o tipo de modelo|contenido del modelo|Consultar modelos de minería de datos|  
|-----------------------------|-------------------|----------------------------|  
|Modelos de reglas de asociación|[Contenido del modelo de minería de datos para los modelos de asociación &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)|[Ejemplos de consultas del modelo de asociación](../../analysis-services/data-mining/association-model-query-examples.md)|  
|Modelos de agrupación en clústeres|[Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Ejemplos de consultas de modelos de agrupación en clústeres](../../analysis-services/data-mining/clustering-model-query-examples.md)|  
|Modelo de árboles de decisión|[Contenido del modelo de minería de datos para los modelos de árboles de decisión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)|[Ejemplos de consultas de modelos de árboles de decisión](../../analysis-services/data-mining/decision-trees-model-query-examples.md)|  
|Modelos de regresión lineal|[Contenido del modelo de minería de datos para los modelos de regresión lineal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)|[Ejemplos de consultas de modelos de regresión lineal](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Modelos de regresión logística|[Contenido del modelo de minería de datos para los modelos de regresión logística &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)|[Ejemplos de consultas de modelos de regresión lineal](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|  
|Modelos Bayes Naïve|[Contenido del modelo de minería de datos para los modelos Bayes naive &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)|[Ejemplos de consultas del modelo Bayes naive](../../analysis-services/data-mining/naive-bayes-model-query-examples.md)|  
|Modelos de red neuronal|[Contenido del modelo de minería de datos para los modelos de red neuronal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)|[Ejemplos de consultas de modelos de red neuronal](../../analysis-services/data-mining/neural-network-model-query-examples.md)|  
|Agrupación en clústeres de secuencia|[Contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)|[Ejemplos de consultas de modelos de clústeres de secuencia](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)|  
|Modelos de serie temporal|[Contenido del modelo de minería de datos para los modelos de serie temporal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)|[Ejemplos de consultas de modelos de serie temporal](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
  
##  <a name="bkmk_Viewing"></a> Herramientas para ver el contenido del modelo de minería de datos  
 Cuando se examina o explora un modelo en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se puede ver la información en el **Visor de árbol de contenido genérico de Microsoft**, que está disponible en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 El Visor de contenido genérico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] muestra las columnas, las reglas, las propiedades, los atributos, los nodos y otro tipo de contenido del modelo utilizando la misma información que está disponible en el conjunto de filas de esquema de contenido del modelo de minería de datos. El conjunto de filas de esquema de contenido es un marco genérico para presentar información detallada sobre el contenido de un modelo de minería de datos. Puede ver el contenido del modelo en cualquier cliente que admita los conjuntos de filas jerárquicos. El visor de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] presenta esta información en un visor de tablas HTML que representa todos los modelos en un formato coherente, lo que facilita la comprensión de la estructura de los modelos que se crean. Para obtener más información, vea [Examinar un modelo usando el Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md).  
  
##  <a name="bkmk_Querying"></a> Herramientas para consultar el contenido del modelo de minería de datos  
 Para recuperar el contenido del modelo de minería de datos, debe crear una consulta que lo use.  
  
 La manera más fácil de crear una consulta de contenido es ejecutar la instrucción DMX siguiente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```  
SELECT * FROM [<mining model name>].CONTENT  
```  
  
 Para obtener más información, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
 También puede consultar el contenido del modelo de minería de datos utilizando los conjuntos de filas de esquema de minería de datos. Un conjunto de filas de esquema es una estructura estándar que los clientes utilizan para detectar, examinar y consultar información sobre las estructuras de minería de datos y los modelos. Puede consultar los conjuntos de filas de esquema utilizando instrucciones de XMLA, Transact-SQL o DMX.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], también puede tener acceso a la información de los conjuntos de filas de esquema de minería de datos abriendo una conexión con la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y consultando las tablas del sistema. Para obtener más información, vea [Conjuntos de filas de esquema de minería de datos &#40;SSA&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md).  
  
## <a name="see-also"></a>Vea también  
 [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)   
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
  
