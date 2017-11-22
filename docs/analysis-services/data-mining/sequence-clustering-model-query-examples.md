---
title: "Ejemplos de consultas de modelo de clústeres de secuencia | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sequence clustering algorithms [Analysis Services]
- content queries [DMX]
- sequence [Analysis Services]
ms.assetid: 64bebcdc-70ab-43fb-8d40-57672a126602
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 97b2c679b61e37cf08299fb64102392bb7ca2202
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sequence-clustering-model-query-examples"></a>Ejemplos de consultas de modelos de clústeres de secuencia
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles sobre la información almacenada en el modelo, o se puede crear una consulta de predicción, que utiliza los patrones del modelo para realizar predicciones según los datos nuevos que se proporcionen. En un modelo de agrupación en clústeres de secuencia, las consultas de contenido normalmente proporcionan detalles adicionales sobre los clústeres que se encontraron o las transiciones dentro de esos clústeres. También se pueden recuperar metadatos sobre el modelo mediante una consulta.  
  
 Las consultas de predicción en un modelo de agrupación en clústeres de secuencia suelen realizar recomendaciones basadas en las secuencias y transiciones, en los atributos sin secuencia que se incluían en el modelo o en una combinación de atributos de secuencia y sin secuencia.  
  
 En esta sección se explica cómo crear consultas para los modelos que se basan en el algoritmo de clústeres de secuencia de Microsoft. Para obtener información general sobre cómo crear consultas, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md).  
  
 **Consultas de contenido**  
  
 [Usar el conjunto de filas de esquema de minería de datos para devolver los parámetros del modelo](#bkmk_Query1)  
  
 [Obtener una lista de secuencias para un estado](#bkmk_Query2)  
  
 [Usar procedimientos almacenados del sistema](#bkmk_Query3)  
  
 **Consultas de predicción**  
  
 [Predecir el estado o estados siguientes](#bkmk_Query4)  
  
##  <a name="bkmk_ContentQueries"></a> Buscar información acerca del modelo de agrupación en clústeres de secuencia  
 Para crear consultas significativas del contenido de un modelo de minería de datos, se debe entender la estructura del contenido del modelo, así como qué tipos de nodo almacenan información y de qué clase es esta. Para más información, vea [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
###  <a name="bkmk_Query1"></a> Consulta de prueba 1: usar el conjunto de filas de esquema de minería de datos para devolver los parámetros del modelo  
 Al consultar el conjunto de filas de esquema de minería de datos, se pueden encontrar varias clases de información sobre el modelo, por ejemplo los metadatos básicos, la fecha y la hora en que el modelo se creó y se procesó por última vez, el nombre de la estructura de minería de datos en que se basa el modelo y el nombre de la columna que se usa como atributo de predicción.  
  
 La consulta siguiente devuelve los parámetros que se usaron para generar y entrenar el modelo, `[Sequence Clustering]`. Puede crear este modelo en la lección 5 de [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c).  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Sequence Clustering'  
```  
  
 Resultados del ejemplo:  
  
|MINING_PARAMETERS|  
|------------------------|  
|CLUSTER_COUNT=15,MINIMUM_SUPPORT=10,MAXIMUM_STATES=100,MAXIMUM_SEQUENCE_STATES=64|  
  
 Observe que este modelo se generó con el valor predeterminado 10 para CLUSTER_COUNT. Al especificar un número de clústeres distinto de cero en CLUSTER_COUNT, el algoritmo trata este número como una sugerencia del número aproximado de clústeres que buscar. Sin embargo, en el proceso de análisis, el algoritmo puede buscar más o menos clústeres. En este caso, el algoritmo encontró que era más apropiado usar 15 clústeres para los datos de entrenamiento. Por consiguiente, la lista de valores de parámetros para el modelo completado notifica el recuento de clústeres tal y como el algoritmo determina, y no el valor pasado al crear el modelo.  
  
 ¿Cómo se diferencia este comportamiento de permitir que el algoritmo determine el mejor número de clústeres? Como experimento, puede crear otro modelo de agrupación en clústeres que use estos mismos datos, pero establecer CLUSTER_COUNT en 0. Si hace esto, el algoritmo detecta 32 clústeres. Por consiguiente, si usa 10 como valor predeterminado de CLUSTER_COUNT, restringe el número de resultados.  
  
 De forma predeterminada se utiliza el valor 10 porque al reducir el número de clústeres se facilita la exploración y comprensión de las agrupaciones de los datos. Sin embargo, cada modelo y conjunto de datos son diferentes. Puede que desee experimentar con números de clústeres diferentes para ver qué valor de parámetro produce el modelo más preciso.  
  
###  <a name="bkmk_Query2"></a> Consulta de prueba 2: obtener una lista de secuencias para un estado  
 El contenido del modelo de minería de datos almacena las secuencias que se encuentran en los datos de entrenamiento como un primer estado junto con una lista de todos los segundos estados relacionados. El primer estado se utiliza como etiqueta para la secuencia y los segundos estados relacionados se denominan transiciones.  
  
 Por ejemplo, la consulta siguiente devuelve la lista completa de los primeros estados del modelo, antes de que las secuencias se agrupen en clústeres.  Puede obtener esta lista devolviendo la lista de secuencias (NODE_TYPE = 13) que tienen el nodo raíz del modelo como elemento primario (PARENT_UNIQUE_NAME = 0). La palabra clave FLATTENED facilita la lectura de los resultados.  
  
> [!NOTE]  
>  El nombre de las columnas, PARENT_UNIQUE_NAME, Support y Probability deben ir entre corchetes para distinguirse de las palabras claves reservadas con la misma denominación.  
  
```  
SELECT FLATTENED NODE_UNIQUE_NAME,  
(SELECT ATTRIBUTE_VALUE AS [Product 1],  
[Support] AS [Sequence Support],   
[Probability] AS [Sequence Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_TYPE = 13  
AND [PARENT_UNIQUE_NAME] = 0  
```  
  
 Resultados parciales:  
  
|NODE_UNIQUE_NAME|Producto 1|Compatibilidad de la secuencia|Probabilidad de la secuencia|  
|------------------------|---------------|----------------------|--------------------------|  
|1081327|Missing|0|#######|  
|1081327|All-Purpose Bike Stand|17|0.00111|  
|1081327|Bike Wash|64|0.00418|  
|1081327|(se omiten las filas 4 a 36)|||  
|1081327|Women's Mountain Shorts|506|0.03307|  
  
 La lista de secuencias del modelo siempre está ordenada alfabéticamente en orden ascendente. La ordenación de las secuencias es importante porque puede encontrar las transiciones relacionadas examinando el número de orden de la secuencia. El valor **Missing** siempre es la transición 0.  
  
 Por ejemplo, en los resultados anteriores, el producto "Women's Mountain Shorts" es el número de secuencia 37 en el modelo. Puede utilizar esa información para ver todos los productos que se compraron alguna vez después de "Women's Mountain Shorts".  
  
 Para ello, en primer lugar hace referencia al valor devuelto para NODE_UNIQUE_NAME en la consulta anterior, para obtener el identificador del nodo que contiene todas las secuencias para el modelo. Este valor se pasa a la consulta como identificador del nodo primario, para obtener solo las transiciones incluidas en este nodo, que resulta que contiene una lista de secuencias para el modelo. Sin embargo, si deseara ver la lista de transiciones para un clúster concreto, podría pasar el identificador del nodo de clúster y solo vería las secuencias asociadas a ese clúster.  
  
```  
SELECT NODE_UNIQUE_NAME  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_DESCRIPTION = 'Transition row for sequence state 37'  
AND [PARENT_UNIQUE_NAME] = '1081327'  
```  
  
 Resultados del ejemplo:  
  
|NODE_UNIQUE_NAME|  
|------------------------|  
|1081365|  
  
 El nodo representado por este identificador contiene una lista de las secuencias que siguen al producto "Women's Mountain Shorts", junto con los valores de probabilidad y compatibilidad.  
  
```  
SELECT FLATTENED  
(SELECT ATTRIBUTE_VALUE AS Product2,  
[Support] AS [P2 Support],  
[Probability] AS [P2 Probability]  
FROM NODE_DISTRIBUTION) AS t  
FROM [Sequence Clustering].CONTENT  
WHERE NODE_UNIQUE_NAME = '1081365'  
```  
  
 Resultados del ejemplo:  
  
|t.Product2|t.P2 Support|t.P2 Probability|  
|----------------|------------------|----------------------|  
|Missing|230.7419|0.456012|  
|Classic Vest|8.16129|0.016129|  
|Cycling Cap|60.83871|0.120235|  
|Half-Finger Gloves|30.41935|0.060117|  
|Long-Sleeve Logo Jersey|86.80645|0.171554|  
|Racing Socks|28.93548|0.057185|  
|Short-Sleeve Classic Jersey|60.09677|0.118768|  
  
 Observe que la compatibilidad de las diversas secuencias relacionadas con Women's Mountain Shorts es 506 en el modelo. Los valores de compatibilidad para las transiciones también suman 506. Sin embargo, las cifras no son números enteros, lo que parece un poco extraño si se espera que la compatibilidad represente simplemente un recuento de los casos que contienen cada transición. Sin embargo, dado que el método para crear clústeres calcula la pertenencia parcial, la probabilidad de cualquier transición dentro de un clúster debe estar compensada por su probabilidad de pertenecer a ese clúster concreto.  
  
 Por ejemplo, si hay cuatro clústeres, una secuencia determinada podría tener una posibilidad del 40% de pertenecer al clúster 1, una posibilidad del 30% de pertenecer al clúster 2, una posibilidad del 20% de pertenecer al grupo 3 y una posibilidad del 10% de pertenecer al clúster 4. Después de que el algoritmo determine el clúster al que es más probable que la transición pertenezca, compensa las probabilidades dentro del clúster con la probabilidad del clúster anterior.  
  
###  <a name="bkmk_Query3"></a> Consulta de ejemplo 3: usar procedimientos almacenados del sistema  
 En estos ejemplos de consultas se puede ver que la información almacenada en el modelo es compleja y que podría ser necesario crear varias consultas para obtener la información que precisa. Sin embargo, el visor de agrupaciones en clústeres de secuencia de Microsoft proporciona un conjunto eficaz de herramientas para examinar gráficamente la información contenida en un modelo de agrupación en clústeres de secuencia y también puede utilizar el visor para consultar y explorar en profundidad en el modelo.  
  
 En la mayoría de los casos, la información que se presenta en el visor de agrupaciones en clústeres de secuencia de Microsoft se crea utilizando los procedimientos almacenados de sistema de Analysis Services para consultar el modelo. Puede escribir las consultas de Extensiones de minería de datos (DMX) con el contenido del modelo para recuperar la misma información, pero los procedimientos almacenados del sistema de Analysis Services proporcionan un acceso directo conveniente para los modelos de prueba o exploración.  
  
> [!NOTE]  
>  Los procedimientos almacenados del sistema se utilizan para el procesamiento interno en el servidor y los clientes que Microsoft proporciona para interactuar con el servidor de Analysis Services. Por consiguiente, Microsoft se reserva el derecho de cambiarlos en cualquier momento. Aunque se describen aquí por comodidad, no admitimos su uso en un entorno de producción. Para asegurarse de la estabilidad y compatibilidad en un entorno de producción, debería escribir siempre sus propias consultas utilizando DMX.  
  
 En esta sección se proporcionan algunos ejemplos de cómo utilizar los procedimientos almacenados del sistema para crear consultas con un modelo de agrupación en clústeres de secuencia:  
  
#### <a name="cluster-profiles-and-sample-cases"></a>Perfiles de clústeres y casos de ejemplo  
 La pestaña Perfiles del clúster muestra una lista de los clústeres del modelo, el tamaño de cada clúster y un histograma que indica los estados incluidos en el clúster. Puede usar dos procedimientos almacenados del sistema en las consultas para recuperar información similar:  
  
-   `GetClusterProfile` devuelve las características del clúster con toda la información que se encuentra en la tabla NODE_DISTRIBUTION para el clúster.  
  
-   `GetNodeGraph` devuelve los nodos y bordes que se pueden utilizar para construir una representación gráfica matemática de los clústeres, que se corresponde con lo que se ve en la primera pestaña de la vista de agrupación en clústeres de secuencia. Los nodos son los clústeres y los bordes representan los pesos o intensidad.  
  
 En el ejemplo siguiente se muestra cómo utilizar el procedimiento almacenado del sistema `GetClusterProfiles`para devolver todos los clústeres del modelo, con sus perfiles respectivos. Este procedimiento almacenado ejecuta una serie de instrucciones DMX que devuelven el conjunto completo de perfiles en el modelo. Sin embargo, para utilizar este procedimiento almacenado, debe conocer la dirección del modelo.  
  
 `CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('Sequence Clustering', 2147483647, 0)`  
  
 En el ejemplo siguiente se muestra cómo recuperar el perfil para un clúster concreto, Cluster 12, utilizando el procedimiento almacenado del sistema `GetNodeGraph`y especificando el identificador del clúster, que normalmente es igual al número del nombre del clúster.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','12',0)  
```  
  
 Si omite el identificador del clúster, como se muestra en la consulta siguiente, `GetNodeGraph` devuelve una lista ordenada y sin estructura jerárquica de todos los perfiles del clúster:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetNodeGraph('Sequence Clustering','',0)  
```  
  
 La pestaña **Perfiles del clúster** también muestra un histograma de casos de ejemplo de modelos. Estos casos de ejemplo representan los casos idealizados para el modelo. Estos casos no se almacenan en el modelo de la misma manera que los datos de entrenamiento; debe utilizar una sintaxis especial para recuperar los casos de ejemplo para el modelo.  
  
```  
SELECT * FROM [Sequence Clustering].SAMPLE_CASES WHERE IsInNode('12')  
```  
  
 Para más información, vea [SELECT FROM &#60;modelo&#62;.SAMPLE_CASES &#40;DMX&#41;](../../dmx/select-from-model-sample-cases-dmx.md).  
  
#### <a name="cluster-characteristics-and-cluster-discrimination"></a>Características del clúster y Distinción del clúster  
 La pestaña **Características del clúster** resume los atributos principales de cada clúster, clasificados por probabilidad. Puede averiguar cuántos casos pertenecen a un clúster y cómo es la distribución de casos en el clúster: Cada característica tiene cierta compatibilidad. Para ver las características de un clúster determinado, debe conocer su identificador.  
  
 En los ejemplos siguientes se usa el procedimiento almacenado del sistema `GetClusterCharacteristics`para devolver todas las características de Cluster 12 que tienen una puntuación de probabilidad por encima del umbral especificado de 0,0005.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','12',0.0005)  
```  
  
 Para devolver las características de todos los clústeres, puede dejar vacío el identificador del clúster.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('Sequence Clustering','',0.0005)  
```  
  
 En el ejemplo siguiente se llama al procedimiento almacenado del sistema `GetClusterDiscrimination` para comparar las características de Cluster 1 y Cluster 12.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('Sequence Clustering','1','12',0.0005,true)  
```  
  
 Si desea escribir su propia consulta DMX para comparar dos clústeres o comparar un clúster con su complemento, primero debe recuperar un conjunto de características y, a continuación, recuperar las características para el clúster concreto en que está interesado y comparar los dos conjuntos. Este escenario es más complicado y normalmente requiere cierto procesamiento del cliente.  
  
#### <a name="states-and-transitions"></a>Estados y transiciones  
 La pestaña **Transiciones de estado** de Agrupación en clústeres de secuencia de Microsoft realiza las consultas complicadas en el back-end para recuperar y comparar las estadísticas de clústeres diferentes. Para reproducir estos resultados, se requiere una consulta más compleja y el procesamiento del cliente.  
  
 Sin embargo, puede utilizar las consultas DMX descritas en el ejemplo 2 de la sección [Consultas de contenido](#bkmk_ContentQueries)para recuperar las probabilidades y estados de las secuencias o de transiciones individuales.  
  
## <a name="using-the-model-to-make-predictions"></a>Usar el modelo para realizar predicciones  
 Las consultas de predicción en un modelo de agrupación en clústeres de secuencia pueden utilizar muchas de las funciones de predicción que se utilizan con otros modelos de agrupación en clústeres. Además, puede usar la función de predicción especial, [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md), para realizar recomendaciones o predecir los estados siguientes.  
  
###  <a name="bkmk_Query4"></a> Consulta de ejemplo 4: predecir el estado o estados siguientes  
 Puede usar la función [PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md) para predecir el siguiente estado más probable según un valor proporcionado. También puede predecir varios de los estados siguientes: por ejemplo, puede devolver una lista de los tres primeros productos que es probable que un cliente compre, para presentar una lista de recomendaciones.  
  
 La consulta de ejemplo siguiente es una consulta de predicción singleton que devuelve las cinco primeras predicciones, junto con su probabilidad. Dado que el modelo incluye una tabla anidada, `[v Assoc Seq Line Items]`, debe utilizarla como referencia al realizar las predicciones. Además, al proporcionar los valores como entrada, debe unir tanto la tabla de casos como las columnas de la tabla anidadas, como se muestra en las instrucciones SELECT anidadas.  
  
```  
SELECT FLATTENED PredictSequence([v Assoc Seq Line Items], 7)  
FROM [Sequence Clustering]  
NATURAL PREDICTION JOIN  
(SELECT  (SELECT 1 as [Line Number],  
   'All-Purpose Bike Stand' as [Model]) AS [v Assoc Seq Line Items])   
AS t  
```  
  
 Resultados del ejemplo:  
  
|Expression.$Sequence|Expression.Line Number|Expression.Model|  
|--------------------------|----------------------------|----------------------|  
|1||Cycling Cap|  
|2||Cycling Cap|  
|3||Sport-100|  
|4||Long-Sleeve Logo Jersey|  
|5||Half-Finger Gloves|  
|6||All-Purpose Bike Stand|  
|7||All-Purpose Bike Stand|  
  
 Hay tres columnas en los resultados, aunque podría esperarse que hubiera solo una, porque la consulta siempre devuelve una columna para la tabla de casos. Aquí los resultados no tienen una estructura jerárquica; de lo contrario, la consulta devolvería una única columna que contuviera dos columnas de tabla anidada.  
  
 $sequence es la columna que devuelve de forma predeterminada la función `PredictSequence` para ordenar los resultados de la predicción. La columna `[Line Number]`se necesita para hacer coincidir las claves de secuencia en el modelo, pero las claves no se devuelven.  
  
 Es interesante ver que las secuencias predichas en primer lugar, después de All-Purpose Bike Stand, son Cycling Cap y Cycling Cap. Esto no es un error. Según cómo se presenten los datos al cliente y cómo se agrupen al entrenar el modelo, es muy posible que haya secuencias de este tipo. Por ejemplo, un cliente podría comprar una gorra de ciclismo (roja) y después otra (azul), o comprar dos seguidas si no hay ninguna manera de especificar la cantidad.  
  
 Los valores de las filas 6 y 7 son marcadores de posición. Al llegar al fin de la cadena de transiciones posibles, en lugar de terminar los resultados de la predicción, el valor que se pasó como entrada se agrega a los resultados. Por ejemplo, si aumentara el número de predicciones a 20, los valores para las filas 6 a 20 serían todos los mismos, All-Purpose Bike Stand.  
  
## <a name="function-list"></a>Lista de funciones  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. Sin embargo, el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite las funciones adicionales que se enumeran en la tabla siguiente.  
  
|||  
|-|-|  
|función de predicción|Uso|  
|[Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md)|Devuelve el clúster que tiene la mayor probabilidad de contener el caso de entrada.|  
|[ClusterDistance &#40;DMX&#41;](../../dmx/clusterdistance-dmx.md)|Devuelve la distancia del caso de entrada con relación al clúster especificado o, si no se ha especificado ninguno, la distancia del caso de entrada del clúster más probable.<br /><br /> Esta función se puede usar con cualquier tipo de modelo de agrupación en clústeres (EM, mediana-K, etc.), pero los resultados difieren según el algoritmo.|  
|[ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)|Devuelve la probabilidad de que el caso de entrada pertenezca al clúster especificado.|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|Indica si el nodo especificado contiene el caso actual.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Devuelve la probabilidad ajustada de un estado especificado.|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|Predice los miembros de asociaciones.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md)|Devuelve la probabilidad de que un caso de entrada se ajuste al modelo existente.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Devuelve una tabla que representa un histograma para la predicción de una columna determinada.|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|Devuelve el Node_ID del nodo en que está clasificado el caso.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Devuelve la probabilidad de un estado especificado.|  
|[PredictSequence &#40;DMX&#41;](../../dmx/predictsequence-dmx.md)|Predice valores de secuencia futuros para un conjunto de datos de secuencia especificado.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Devuelve la desviación estándar predicha para la columna especificada.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|Devuelve el valor de soporte de un estado especificado.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Devuelve la varianza de una columna especificada.|  
  
 Para consultar una lista de las funciones comunes a todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)], vea [Funciones de predicción generales &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md). Para más información sobre la sintaxis de funciones específicas, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)   
 [Referencia técnica del algoritmo de agrupación en clústeres de secuencia de Microsoft](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Microsoft Sequence Clustering Algorithm](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres de secuencia &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
