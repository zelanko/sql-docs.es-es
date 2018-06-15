---
title: Ejemplos de consultas de modelo de agrupación en clústeres | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6e415c0b82738ec153b20cb79e19af59bacba16
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019432"
---
# <a name="clustering-model-query-examples"></a>Ejemplos de consultas de modelos de agrupación en clústeres
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Al crear una consulta en un modelo de minería de datos, puede recuperar metadatos sobre el modelo o crear una consulta de contenido que proporcione detalles sobre los patrones detectados en el análisis. También puede crear una consulta de predicción, que usa los patrones del modelo para realizar predicciones para los nuevos datos. Cada tipo de consulta proporcionará información diferente. Por ejemplo, una consulta de contenido puede proporcionar detalles adicionales sobre los clústeres encontrados, mientras que una consulta de predicción puede indicar a qué clúster pertenece con mayor probabilidad un nuevo punto de datos.  
  
 En esta sección se explica cómo crear consultas en modelos basados en el algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de contenido**  
  
 [Obtener metadatos del modelo usando DMX](#bkmk_Query1)  
  
 [Recuperar metadatos del modelo a partir del conjunto de filas de esquema](#bkmk_Query2)  
  
 [Devolver un clúster o una lista de clústeres](#bkmk_Query3)  
  
 [Devolver los atributos de un clúster](#bkmk_Query4)  
  
 [Devolver un perfil de clúster usando los procedimientos almacenados del sistema](#bkmk_Query5)  
  
 [Buscar los factores de distinción para un clúster](#bkmk_Query6)  
  
 [Devolver los casos que pertenecen a un clúster](#bkmk_Query7)  
  
 **Consultas de predicción**  
  
 [Predecir resultados de un modelo de clústeres](#bkmk_Query8)  
  
 [Determinar la pertenencia al clúster](#bkmk_Query9)  
  
 [Devolver todos los clústeres posibles con probabilidad y distancia](#bkmk_Query10)  
  
##  <a name="bkmk_top2"></a> Buscar información sobre el modelo  
 Todos los modelos de minería de datos exponen el contenido aprendido por el algoritmo de acuerdo con un esquema normalizado, el conjunto de filas de esquema del modelo de minería de datos. Puede crear consultas en el conjunto de filas de esquema del modelo de minería de datos usando instrucciones de Extensiones de minería de datos (DMX). En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], también puede consultar directamente los conjuntos de filas de esquema como tablas del sistema.  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query1"></a> Consulta de ejemplo 1: obtener metadatos del modelo usando DMX  
 La consulta siguiente devuelve metadatos básicos sobre el modelo de agrupación en clústeres, `TM_Clustering`, que creó en el Tutorial básico de minería de datos. Los metadatos disponibles en el nodo primario de un modelo de agrupación en clústeres incluyen el nombre del modelo, la base de datos en la que se encuentra almacenado el modelo y el número de nodos secundarios existentes en el modelo. Esta consulta usa una consulta de contenido DMX para recuperar los metadatos del nodo primario del modelo:  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  El nombre de la columna CHILDREN_CARDINALITY debe ir entre corchetes para distinguirlo de la palabra clave reservada de Expresiones multidimensionales (MDX) del mismo nombre.  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|MODEL_CATALOG|TM_Clustering|  
|MODEL_NAME|Adventure Works DW|  
|NODE_CAPTION|Cluster Model|  
|NODE_SUPPORT|12939|  
|CHILDREN_CARDINALITY|10|  
|NODE_DESCRIPTION|Todos|  
  
 Para ver una definición de lo que significan estas columnas en un modelo de agrupación en clústeres, vea [Contenido del modelo de minería de datos para modelos de agrupaciones en clúster &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> Consulta de ejemplo 2: recuperar metadatos del modelo a partir del conjunto de filas de esquema  
 Mediante una consulta al conjunto de filas de esquema de minería de datos, puede obtener la misma información que a través de una consulta de contenido DMX. Sin embargo, el conjunto de filas de esquema proporciona algunas columnas adicionales. Esto incluye los parámetros que se usaron cuando se creó el modelo, la fecha y la hora en que se procesó el modelo por última vez, y el propietario del modelo.  
  
 En el ejemplo siguiente se devuelve la fecha en la que se creó, modificó y procesó el modelo por última vez, junto con los parámetros de agrupación en clústeres que se usaron para generar el modelo y el tamaño del conjunto de entrenamiento. Esta información puede ser útil para documentar el modelo o para determinar qué opciones de agrupación en clústeres se usaron para crear un modelo existente.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Clustering'  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|MODEL_NAME|TM_Clustering|  
|DATE_CREATED|10/12/2007 7:42:51 PM|  
|LAST_PROCESSED|10/12/2007 8:09:54 PM|  
|PREDICTION_ENTITY|Bike Buyer|  
|MINING_PARAMETERS|CLUSTER_COUNT=10,<br /><br /> CLUSTER_SEED=0,<br /><br /> CLUSTERING_METHOD=1,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100,<br /><br /> MINIMUM_SUPPORT=1,<br /><br /> MODELLING_CARDINALITY=10,<br /><br /> SAMPLE_SIZE=50000,<br /><br /> STOPPING_TOLERANCE=10|  
  
 [Volver al principio](#bkmk_top2)  
  
## <a name="finding-information-about-clusters"></a>Buscar información sobre clústeres  
 Las consultas de contenido más útiles que se realizan en los modelos de agrupación en clústeres generalmente devuelven el mismo tipo de información que se puede examinar usando el **Visor de clústeres**. Esto incluye perfiles del clúster, características del clúster y distinción del clúster. En esta sección se proporcionan ejemplos de consultas que recuperan esta información.  
  
###  <a name="bkmk_Query3"></a> Consulta de ejemplo 3: devolver un clúster o una lista de clústeres  
 Dado que todos los clústeres tienen un tipo de nodo 5, se puede recuperar con facilidad una lista de los clústeres consultando solamente los nodos de ese tipo en el contenido del modelo. También se pueden filtrar los nodos devueltos según la probabilidad o el soporte, tal y como se muestra en este ejemplo.  
  
```  
SELECT NODE_NAME, NODE_CAPTION ,NODE_SUPPORT, NODE_DESCRIPTION  
FROM TM_Clustering.CONTENT  
WHERE NODE_TYPE = 5 AND NODE_SUPPORT > 1000  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|NODE_NAME|002|  
|NODE_CAPTION|Clúster 2|  
|NODE_SUPPORT|1649|  
|NODE_DESCRIPTION|English Education=Graduate Degree , 32 <=Age <=48 , Number Cars Owned=0 , 35964.0771121808 <=Yearly Income <=97407.7163393957 , English Occupation=Professional , Commute Distance=2-5 Miles , Region=North America , Bike Buyer=1 , Number Children At Home=0 , Number Cars Owned=1 , Commute Distance=0-1 Miles , English Education=Bachelors , Total Children=1 , Number Children At Home=2 , English Occupation=Skilled Manual , Marital Status=S , Total Children=0 , House Owner Flag=0 , Gender=F , Total Children=2 , Region=Pacific|  
  
 Los atributos que definen el clúster se pueden encontrar en dos columnas del conjunto de filas de esquema de minería de datos.  
  
-   La columna NODE_DESCRIPTION contiene una lista de atributos separados por comas. Observe que la lista de atributos se puede abreviar con fines de visualización.  
  
-   La tabla anidada de la columna NODE_DISTRIBUTION contiene la lista completa de atributos para el clúster. Si el cliente no admite conjuntos de filas jerárquicos, se puede devolver la tabla anidada anteponiendo la palabra clave FLATTENED a la lista de columnas de la instrucción SELECT. Para más información sobre el uso de la palabra clave FLATTENED, vea [SELECT FROM &#60;model&#62;.CONTENT &#40;DMX&#41;](../../dmx/select-from-model-content-dmx.md).  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query4"></a> Consulta de ejemplo 4: devolver atributos para un clúster  
 Para cada clúster, el **Visor de clústeres** muestra un perfil con los atributos y sus valores. El visor también muestra un histograma con la distribución de valores para el conjunto completo de casos del modelo. Si está examinando el modelo en el visor, puede copiar fácilmente el histograma de la Leyenda de minería de datos y, a continuación, pegarlo en un documento de Excel o de Word. También puede usar el panel Características del clúster del visor para comparar gráficamente los atributos de clústeres diferentes.  
  
 Sin embargo, si necesita obtener valores para varios clústeres a la vez, le resultará más fácil consultar el modelo. Por ejemplo, al examinar el modelo, podrá observar que los dos clústeres superiores difieren en lo que respecta al atributo `Number Cars Owned`. Por consiguiente, desea extraer los valores para cada clúster.  
  
```  
SELECT TOP 2 NODE_NAME,   
(SELECT ATTRIBUTE_VALUE, [PROBABILITY] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Number Cars Owned')  
AS t  
FROM [TM_Clustering].CONTENT  
WHERE NODE_TYPE = 5  
```  
  
 La primera línea del código especifica que solamente desea los dos clústeres superiores.  
  
> [!NOTE]  
>  De forma predeterminada, los clústeres se ordenan por soporte. Por tanto, se puede omitir la columna NODE_SUPPORT.  
  
 La segunda línea del código agrega una instrucción sub-SELECT que solamente devuelve ciertas columnas de la columna de tabla anidada. Además, restringe las filas de la tabla anidada a las que están relacionadas con el atributo de destino, `Number Cars Owned`. Para simplificar la visualización, la tabla anidada tiene un alias.  
  
> [!NOTE]  
>  La columna de tabla anidada, `PROBABILITY`, debe ir entre corchetes porque también es el nombre de una palabra clave reservada de MDX.  
>   
>  Resultados del ejemplo:  
  
|NODE_NAME|T.ATTRIBUTE_VALUE|T.PROBABILITY|  
|----------------|------------------------|-------------------|  
|001|2|0.829207754|  
|001|1|0.109354156|  
|001|3|0.034481552|  
|001|4|0.013503302|  
|001|0|0.013453236|  
|001|Missing|0|  
|002|0|0.576980023|  
|002|1|0.406623939|  
|002|2|0.016380082|  
|002|3|1.60E-05|  
|002|4|0|  
|002|Missing|0|  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> Consulta de ejemplo 5: devolver un perfil de clúster usando los procedimientos almacenados del sistema  
 Como método abreviado, en lugar de escribir sus propias consultas usando DMX, también puede llamar a los procedimientos almacenados del sistema que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa para trabajar con clústeres. En el ejemplo siguiente se muestra cómo usar los procedimientos almacenados internos para devolver el perfil de un clúster con el identificador 002.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterProfiles('TM_Clustering", '002',0.0005  
```  
  
 De igual forma, puede utilizar un procedimiento almacenado del sistema para devolver las características de un clúster concreto, tal como se muestra en el ejemplo siguiente:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterCharacteristics('TM_Clustering", '009',0.0005  
```  
  
 Resultados del ejemplo:  
  
|Atributos|Valores|Frecuencia|Soporte técnico|  
|----------------|------------|---------------|-------------|  
|Number Children at Home|0|0.999999829076798|899|  
|Region|North America|0.999852875241508|899|  
|Total Children|0|0.993860958572323|893|  
  
> [!NOTE]  
>  Los procedimientos almacenados del sistema de minería de datos son para uso interno y [!INCLUDE[msCoName](../../includes/msconame-md.md)] se reserva el derecho de cambiarlos si lo considera necesario. En un entorno de producción, se recomienda crear las consultas utilizando DMX, AMO o XMLA.  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query6"></a> Consulta de ejemplo 6: buscar factores de distinción para un clúster  
 La pestaña **Distinción del clúster** del **Visor de clústeres** permite comparar fácilmente un clúster con otro, o bien un clúster con el resto de los casos (el complemento del clúster).  
  
 Sin embargo, crear consultas para devolver esta información puede resultar complejo y podría ser necesario algún procesamiento adicional en el cliente para almacenar los resultados temporales y comparar los resultados de dos o más consultas. Como método abreviado, puede utilizar los procedimientos almacenados del sistema.  
  
 La consulta siguiente devuelve una única tabla que indica los factores de distinción primarios entre dos clústeres que tienen los identificadores de nodo 009 y 007. Los atributos con valores positivos favorecen al clúster 009, mientras que los atributos con valores negativos favorecen al clúster 007.  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','007',0.0005,true)  
```  
  
 Resultados del ejemplo:  
  
|Atributos|Valores|Puntuación|  
|----------------|------------|-----------|  
|Region|North America|100|  
|English Occupation|Skilled Manual|94.9003803898654|  
|Region|Europe|-72.5041051379789|  
|English Occupation|Manual|-69.6503163202722|  
  
 Esta es la misma información que se presenta en el gráfico del visor **Distinción del clúster** si selecciona el clúster 9 en la primera lista desplegable y el clúster 7 en la segunda lista desplegable. Para comparar el clúster 9 con su complemento, utilice la cadena vacía en el segundo parámetro, tal como se muestra en el ejemplo siguiente:  
  
```  
CALL System.Microsoft.AnalysisServices.System.DataMining.Clustering.GetClusterDiscrimination('TM_Clustering','009','',0.0005,true)  
```  
  
> [!NOTE]  
>  Los procedimientos almacenados del sistema de minería de datos son para uso interno y [!INCLUDE[msCoName](../../includes/msconame-md.md)] se reserva el derecho de cambiarlos si lo considera necesario. En un entorno de producción, se recomienda crear las consultas utilizando DMX, AMO o XMLA.  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> Consulta de ejemplo 7: devolver casos que pertenecen a un clúster  
 Si se ha habilitado la obtención de detalles en el modelo de minería de datos, puede crear consultas que devuelvan información detallada sobre los casos utilizados en el modelo. Es más, si se ha habilitado la obtención de detalles en la estructura de minería de datos, puede incluir columnas de la estructura interna con la función [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md).  
  
 En el ejemplo siguiente se devuelven dos columnas que se utilizaron en el modelo, Age y Region, y una columna más, First Name, que no se utilizó en el modelo. La consulta solo devuelve casos que se clasificaron en el clúster 1.  
  
```  
SELECT [Age], [Region], StructureColumn('First Name')  
FROM [TM_Clustering].CASES  
WHERE IsInNode('001')  
```  
  
 Para devolver los casos que pertenecen a un clúster, debe conocer el identificador de dicho clúster. Puede obtener el identificador del clúster examinando el modelo en uno de los visores. O bien, puede cambiar el nombre de un clúster para hacer referencia a él de manera más fácil y utilizar dicho nombre en lugar del número de identificador. Sin embargo, tenga en cuenta que los nombres que asigne a un clúster se perderán si se vuelve a procesar el modelo.  
  
 [Volver al principio](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>Realizar predicciones utilizando el modelo  
 Aunque la agrupación en clústeres se utiliza normalmente para describir y entender los datos, la implementación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] también permite realizar una predicción sobre la pertenencia al clúster y devolver probabilidades asociadas a dicha predicción. En esta sección se proporcionan ejemplos de cómo crear consultas de predicción en modelos de agrupación en clústeres. Puede realizar predicciones para varios casos, especificando un origen de datos tabular, o puede proporcionar nuevos valores de uno en uno creando una consulta singleton. Para mayor claridad, todos los ejemplos de esta sección son consultas singleton.  
  
 Para más información sobre la forma de crear consultas de predicción con DMX, vea [Herramientas de consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query8"></a> Consulta de ejemplo 8: predecir resultados de un modelo de agrupación en clústeres  
 Si el modelo de agrupación en clústeres creado contiene un atributo de predicción, puede utilizar el modelo para realizar predicciones sobre los resultados. Sin embargo, el modelo procesa el atributo de predicción de manera diferente dependiendo de si se establece la columna de predicción en **Predict** o en **PredictOnly**. Si establece el uso de la columna en **Predict**, los valores para ese atributo se agregan al modelo de agrupación en clústeres y aparecen como atributos en el modelo finalizado. Sin embargo, si establece el uso de la columna en **PredictOnly**, los valores no se utilizan para crear clústeres. En su lugar, una vez completado el modelo, el algoritmo de clústeres crea nuevos valores para el atributo **PredictOnly** basándose en los clústeres a los que pertenece cada caso.  
  
 La consulta siguiente proporciona al modelo un único caso nuevo, en que la única información sobre el caso es la edad y el género. La instrucción SELECT especifica el par atributo/valor de predicción en que está interesado y la función [PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md) indica la probabilidad de que un caso con esos atributos tenga el resultado deseado.  
  
```  
SELECT  
  [TM_Clustering].[Bike Buyer], PredictProbability([Bike Buyer],1)  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Ejemplo de resultados cuando el uso se establece en **Predict**:  
  
|Bike Buyer|Expresión|  
|----------------|----------------|  
|1|0.592924735740338|  
  
 Ejemplo de resultados cuando el uso se establece en **PredictOnly** y se vuelve a procesar el modelo:  
  
|Bike Buyer|Expresión|  
|----------------|----------------|  
|1|0.55843544003102|  
  
 En este ejemplo, la diferencia en el modelo no es significativa. Sin embargo, a veces puede ser importante para detectar las diferencias entre la distribución real de valores y lo que predice el modelo. La pestaña [PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md) es útil en este escenario, ya que indica la probabilidad de un caso según un modelo específico.  
  
 El número devuelto por la función PredictCaseLikelihood es una probabilidad y, por lo tanto, siempre está comprendido entre 0 y 1, y el valor 0,5 representa un resultado aleatorio. Por consiguiente, una puntuación menor que 0.5 significa que el caso predicho es improbable, dado el modelo, mientras que una puntuación mayor que 0.5 indica que el caso predicho es más probable que se ajuste al modelo.  
  
 Por ejemplo, la consulta siguiente devuelve dos valores que caracterizan la probabilidad de un nuevo caso de ejemplo. El valor no normalizado representa la probabilidad dado el modelo actual. Cuando se utiliza la palabra clave NORMALIZED, la puntuación de probabilidad devuelta por la función se ajusta dividiendo la "probabilidad con el modelo" entre la "probabilidad sin el modelo".  
  
```  
SELECT  
PredictCaseLikelihood(NORMALIZED) AS [NormalizedValue], PredictCaseLikelihood(NONNORMALIZED) AS [NonNormalizedValue]  
FROM  
  [TM_Clustering_PredictOnly]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender]) AS t  
```  
  
 Resultados del ejemplo:  
  
|NormalizedValue|NonNormalizedValue|  
|---------------------|------------------------|  
|5,56438372679893E-11|8,65459953145182E-68|  
  
 Observe que los números de estos resultados se expresan en notación científica.  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query9"></a> Consulta de ejemplo 9: determinar la pertenencia al clúster  
 En este ejemplo se usa la función [Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md) para devolver el clúster al que pertenece con mayor probabilidad el nuevo caso y se usa la función [ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md) para devolver la probabilidad de pertenencia a ese clúster.  
  
```  
SELECT Cluster(), ClusterProbability()  
FROM  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status]) AS t  
```  
  
 Resultados del ejemplo:  
  
|$CLUSTER|Expresión|  
|--------------|----------------|  
|Clúster 2|0.397918596951617|  
  
 **Nota** : de forma predeterminada, la función **ClusterProbability** devuelve la probabilidad del clúster más probable. Sin embargo, puede especificar otro clúster utilizando la sintaxis `ClusterProbability('cluster name')`. Si lo hace, sea consciente de que los resultados de cada función de predicción son independientes de los demás resultados. Por consiguiente, la puntuación de probabilidad en la segunda columna podría hacer referencia a un clúster distinto del clúster mencionado en la primera columna.  
  
 [Volver al principio](#bkmk_top2)  
  
###  <a name="bkmk_Query10"></a> Consulta de ejemplo 10: devolver todos los clústeres posibles con probabilidad y distancia  
 En el ejemplo anterior, la puntuación de probabilidad no fue muy alta. Para determinar si hay un clúster mejor, puede usar la función [PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md) con la función [Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md) para devolver una tabla anidada donde se incluyan todos los clústeres posibles, además de la probabilidad de que el nuevo caso pertenezca a cada clúster. La palabra clave FLATTENED se utiliza para cambiar el conjunto de filas jerárquico por una tabla plana para facilitar la visualización.  
  
```  
SELECT FLATTENED PredictHistogram(Cluster())  
From  
  [TM_Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 40 AS [Age],  
  'F' AS [Gender],  
  'S' AS [Marital Status])  
```  
  
|Expression.$CLUSTER|Expression.$DISTANCE|Expression.$PROBABILITY|  
|-------------------------|--------------------------|-----------------------------|  
|Clúster 2|0.602081403048383|0.397918596951617|  
|Clúster 10|0.719691686785675|0.280308313214325|  
|Clúster 4|0.867772590378791|0.132227409621209|  
|Clúster 5|0.931039872200985|0.0689601277990149|  
|Clúster 3|0.942359230072167|0.0576407699278328|  
|Clúster 6|0.958973668972756|0.0410263310272437|  
|Clúster 7|0.979081275926724|0.0209187240732763|  
|Clúster 1|0.999169044818624|0.000830955181376364|  
|Clúster 9|0.999831227795894|0.000168772204105754|  
|Clúster 8|1|0|  
  
 De forma predeterminada, los resultados se clasifican por probabilidad. Los resultados indican que, aunque la probabilidad para el clúster 2 es bastante baja, este clúster sigue siendo el que mejor se ajusta al nuevo punto de datos.  
  
 **Nota** : la columna adicional, `$DISTANCE`, representa la distancia desde el punto de datos hasta el clúster. De forma predeterminada, el algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] utiliza el método de agrupación en clústeres EM escalable, que asigna varios clústeres a cada punto de datos y clasifica los posibles clústeres.  Sin embargo, si crea el modelo de agrupación en clústeres utilizando el algoritmo mediana-K, solamente se podrá asignar un clúster a cada punto de datos y esta consulta devolverá una sola fila. Es necesario comprender estas diferencias para interpretar los resultados de la función [PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md) . Para más información sobre las diferencias entre la agrupación en clústeres de EM y de mediana-K, vea [Referencia técnica del algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md).  
  
 [Volver al principio](#bkmk_top2)  
  
## <a name="function-list"></a>Lista de funciones  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. Sin embargo, los modelos que se generan usando el algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admiten las funciones adicionales incluidas en la tabla siguiente.  
  
|||  
|-|-|  
|Función de predicción|Uso|  
|[Cluster &#40;DMX&#41;](../../dmx/cluster-dmx.md)|Devuelve el clúster que tiene la mayor probabilidad de contener el caso de entrada.|  
|[ClusterDistance &#40;DMX&#41;](../../dmx/clusterdistance-dmx.md)|Devuelve la distancia del caso de entrada con relación al clúster especificado o, si no se ha especificado ninguno, la distancia del caso de entrada del clúster más probable.<br /><br /> Devuelve la probabilidad de que el caso de entrada pertenezca al clúster especificado.|  
|[ClusterProbability &#40;DMX&#41;](../../dmx/clusterprobability-dmx.md)|Devuelve la probabilidad de que el caso de entrada pertenezca al clúster especificado.|  
|[IsDescendant & #40; DMX & #41;](../../dmx/isdescendant-dmx.md)|Determina si un nodo es un elemento secundario de otro nodo del modelo.|  
|[IsInNode & #40; DMX & #41;](../../dmx/isinnode-dmx.md)|Indica si el nodo especificado contiene el caso actual.|  
|[PredictAdjustedProbability & #40; DMX & #41;](../../dmx/predictadjustedprobability-dmx.md)|Devuelve la probabilidad ponderada.|  
|[PredictAssociation & #40; DMX & #41;](../../dmx/predictassociation-dmx.md)|Predice los miembros de un conjunto de datos asociativo.|  
|[PredictCaseLikelihood &#40;DMX&#41;](../../dmx/predictcaselikelihood-dmx.md)|Devuelve la probabilidad de que un caso de entrada se ajuste al modelo existente.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Devuelve una tabla de valores relacionados con el valor de predicción actual.|  
|[PredictNodeId & #40; DMX & #41;](../../dmx/predictnodeid-dmx.md)|Devuelve el Node_ID de cada caso.|  
|[PredictProbability & #40; DMX & #41;](../../dmx/predictprobability-dmx.md)|Devuelve la probabilidad del valor de predicción.|  
|[PredictStdev & #40; DMX & #41;](../../dmx/predictstdev-dmx.md)|Devuelve la desviación estándar predicha para la columna especificada.|  
|[PredictSupport & #40; DMX & #41;](../../dmx/predictsupport-dmx.md)|Devuelve el valor de soporte de un estado especificado.|  
|[PredictVariance & #40; DMX & #41;](../../dmx/predictvariance-dmx.md)|Devuelve la varianza de una columna especificada.|  
  
 Para más información sobre la sintaxis de funciones específicas, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-clustering-algorithm-technical-reference.md)   
 [Algoritmo de clústeres de Microsoft](../../analysis-services/data-mining/microsoft-clustering-algorithm.md)  
  
  
