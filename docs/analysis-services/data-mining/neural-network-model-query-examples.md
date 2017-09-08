---
title: Ejemplos de consultas de modelo de red neuronal | Documentos de Microsoft
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
- neural network algorithms [Analysis Services]
- content queries [DMX]
- neural network model [Analysis Services]
ms.assetid: 81b06183-620f-4e0c-bc10-532e6a1f0829
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 16343214615687c3a2ac39c9083c867c6d1e91c1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="neural-network-model-query-examples"></a>Ejemplos de consultas de modelos de red neuronal
  Cuando se crea una consulta en un modelo de minería de datos, puede tratarse de una consulta de contenido, que proporciona detalles de los patrones detectados durante el análisis, o de una consulta de predicción, que utiliza los patrones del modelo para realizar predicciones de los nuevos datos. Por ejemplo, una consulta de contenido para un modelo de red neuronal podría recuperar metadatos del modelo, por ejemplo, el número de niveles ocultos. O bien, una consulta de predicción podría sugerir las clasificaciones según una entrada y proporcionar, si se desea, las probabilidades para cada clasificación.  
  
 En esta sección se explica cómo crear consultas para los modelos que se basan en el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Consultas de contenido**  
  
 [Obtener metadatos del modelo usando DMX](#bkmk_Query1)  
  
 [Recuperar metadatos del modelo a partir del conjunto de filas de esquema](#bkmk_Query2)  
  
 [Recuperar los atributos de entrada para el modelo](#bkmk_Query3)  
  
 [Recuperar las ponderaciones del nivel oculto](#bkmk_Query4)  
  
 **Consultas de predicción**  
  
 [Crear una predicción singleton](#bkmk_Query5)  
  
## <a name="finding-information-about-a-neural-network-model"></a>Buscar información sobre un modelo de red neuronal  
 Todos los modelos de minería de datos exponen el contenido aprendido por el algoritmo de acuerdo con un esquema normalizado, el conjunto de filas de esquema del modelo de minería de datos. Esta información proporciona detalles sobre el modelo e incluye los metadatos básicos, las estructuras detectadas en el análisis y los parámetros que se utilizan en el proceso. Puede crear consultas en el contenido del modelo usando instrucciones de Extensiones de minería de datos (DMX).  
  
###  <a name="bkmk_Query1"></a> Consulta de ejemplo 1: obtener metadatos del modelo usando DMX  
 La consulta siguiente devuelve algunos metadatos básicos sobre un modelo que se generó con el algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . En un modelo de red neuronal, el nodo primario del modelo únicamente contiene el nombre del modelo, el nombre de la base de datos en la que se encuentra almacenado el modelo y el número de nodos secundarios. Sin embargo, el nodo de estadísticas marginal (NODE_TYPE = 24) proporciona tanto los metadatos básicos como algunas estadísticas derivadas acerca de las columnas de entrada que se usan en el modelo.  
  
 La siguiente consulta de ejemplo se basa en el modelo de minería creado en el [Tutorial intermedio de minería de datos](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b), denominado `Call Center Default NN`. El modelo utiliza datos de un centro de atención telefónica para explorar las correlaciones posibles entre el personal y el número de llamadas, pedidos e incidencias. La instrucción DMX recupera los datos del nodo de estadísticas marginales del modelo de red neuronal. La consulta incluye la palabra clave FLATTENED, porque las estadísticas de los atributos de entrada de interés están almacenadas en una tabla anidada, NODE_DISTRIBUTION. Sin embargo, si el proveedor de consultas admite conjuntos de filas jerárquicos, no necesita utilizar la palabra clave FLATTENED.  
  
```  
SELECT FLATTENED MODEL_CATALOG, MODEL_NAME,   
(    SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE,  
     [SUPPORT], [PROBABILITY], VALUETYPE   
     FROM NODE_DISTRIBUTION  
) AS t  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 24  
```  
  
> [!NOTE]  
>  Debe incluir entre corchetes el nombre de las columnas de la tabla anidada SUPPORT y PROBABILITY para distinguirlas de las palabras clave reservadas homónimas.  
  
 Resultados del ejemplo:  
  
|MODEL_CATALOG|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|--------------------|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|Missing|0|0|1|  
|Adventure Works DW Multidimensional 2012|Call Center NN|Average Time Per Issue|<64.7094100096|11|0.407407407|5|  
  
 Para ver una definición del significado de las columnas del conjunto de filas de esquema en el contexto de un modelo de red neuronal, vea [Contenido del modelo de minería de datos para los modelos de red neuronal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
###  <a name="bkmk_Query2"></a> Consulta de ejemplo 2: recuperar metadatos del modelo a partir del conjunto de filas de esquema  
 Mediante una consulta al conjunto de filas de esquema de minería de datos, puede obtener la misma información que a través de una consulta de contenido DMX. Sin embargo, el conjunto de filas de esquema proporciona algunas columnas adicionales. La consulta del ejemplo siguiente devuelve la fecha en que el modelo fue creado, modificado y procesado por última vez. La consulta también devuelve las columnas de predicción, que no están disponibles con facilidad en el contenido del modelo, y los parámetros que se usaron para generarlo. Esta información puede ser útil para documentar el modelo.  
  
```  
SELECT MODEL_NAME, DATE_CREATED, LAST_PROCESSED, PREDICTION_ENTITY, MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Call Center Default NN'  
```  
  
 Resultados del ejemplo:  
  
|||  
|-|-|  
|MODEL_NAME|Call Center Default NN|  
|DATE_CREATED|1/10/2008 5:07:38 PM|  
|LAST_PROCESSED|1/10/2008 5:24:02 PM|  
|PREDICTION_ENTITY|Average Time Per Issue,<br /><br /> Grade Of Service,<br /><br /> Number Of Orders|  
|MINING_PARAMETERS|HOLDOUT_PERCENTAGE=30, HOLDOUT_SEED=0,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255, MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_STATES=100, SAMPLE_SIZE=10000, HIDDEN_NODE_RATIO=4|  
  
###  <a name="bkmk_Query3"></a> Consulta de ejemplo 3: recuperar los atributos de entrada para el modelo  
 Puede recuperar los pares de entradas atributo-valor que se usaron para crear el modelo consultando los nodos secundarios (NODE_TYPE = 20) del nivel de entrada (NODE_TYPE = 18). La consulta siguiente devuelve una lista de atributos de entrada a partir de las descripciones de los nodos.  
  
```  
SELECT NODE_DESCRIPTION  
FROM [Call Center Default NN].CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 Resultados del ejemplo:  
  
|NODE_DESCRIPTION|  
|-----------------------|  
|Average Time Per Issue=64.7094100096 - 77.4002099712|  
|Day Of Week=Fri.|  
|Level 1 Operators|  
  
 Aquí solo se muestran unas filas representativas de los resultados. Sin embargo, puede ver que NODE_DESCRIPTION proporciona información ligeramente diferente que depende del tipo de datos del atributo de entrada.  
  
-   Si el atributo es un valor discreto o de datos discretos, se devuelven tanto el atributo como su valor o intervalo de datos discretos.  
  
-   Si el atributo es un tipo de datos numéricos continuo, NODE_DESCRIPTION solamente contiene el nombre de atributo. Sin embargo, puede recuperar la tabla NODE_DISTRIBUTION anidada para obtener la media o devuelve NODE_RULE para obtener los valores máximo y mínimo del intervalo numérico.  
  
 La consulta siguiente muestra cómo consultar la tabla NODE_DISTRIBUTION anidada para devolver los atributos en una columna y sus valores en otra. En los atributos continuos, el valor del atributo se representa mediante su media.  
  
```  
SELECT FLATTENED   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE  
FROM NODE_DISTRIBUTION) as t  
FROM [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 21  
```  
  
 Resultados del ejemplo:  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|  
|-----------------------|------------------------|  
|Average Time Per Issue|64.7094100096 - 77.4002099712|  
|Day Of Week|Fri.|  
|Level 1 Operators|3.2962962962963|  
  
 Los valores del intervalo mínimo y máximo están almacenados en la columna NODE_RULE y se representan como un fragmento XML, como se muestra en el ejemplo siguiente:  
  
```  
<NormContinuous field="Level 1 Operators">    
  <LinearNorm orig="2.83967303681711" norm="-1" />    
  <LinearNorm orig="3.75291955577548" norm="1" />    
</NormContinuous>    
```  
  
###  <a name="bkmk_Query4"></a> Consulta de ejemplo 4: recuperar los pesos del nivel oculto  
 El contenido de un modelo de red neuronal se estructura en un modo que facilita la recuperación de los detalles sobre cualquier nodo de la red. Es más, los números de identificadores de los nodos proporcionan información que ayuda a identificar las relaciones entre los tipos de nodo.  
  
 La consulta siguiente demuestra cómo recuperar los coeficientes que están almacenados bajo un nodo determinado del nivel oculto. El nivel oculto está compuesto de un nodo de organizador (NODE_TYPE = 19), que solo contiene metadatos, y varios nodos secundarios (NODE_TYPE = 22), que contienen los coeficientes de las diversas combinaciones de atributos y valores. Esta consulta devuelve solo los nodos de coeficiente.  
  
```  
SELECT FLATTENED TOP 1 NODE_UNIQUE_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM  [Call Center Default NN -- Predict Service and Orders].CONTENT  
WHERE NODE_TYPE = 22  
AND [PARENT_UNIQUE_NAME] = '40000000200000000' FROM [Call Center Default NN].CONTENT  
```  
  
 Resultados del ejemplo:  
  
|NODE_UNIQUE_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|------------------------|-----------------------|------------------------|-----------------|  
|70000000200000000|6000000000000000a|-0.178616518|7|  
|70000000200000000|6000000000000000b|-0.267561918|7|  
|70000000200000000|6000000000000000c|0.11069497|7|  
|70000000200000000|6000000000000000d|0.123757712|7|  
|70000000200000000|6000000000000000e|0.294565343|7|  
|70000000200000000|6000000000000000f|0.22245318|7|  
|70000000200000000||0.188805045|7|  
  
 Los resultados parciales mostrados aquí demuestran cómo el contenido del modelo de red neuronal relaciona el nodo oculto con los nodos de entrada.  
  
-   Los nombres únicos de los nodos en el nivel oculto siempre empiezan por 70000000.  
  
-   Los nombres únicos de los nodos en el nivel de entrada siempre empiezan por 60000000.  
  
 Por tanto, estos resultados indican que al nodo denotado por el identificador 70000000200000000 se le habían pasado seis coeficientes diferentes (VALUETYPE = 7). Los valores de los coeficientes están en la columna ATTRIBUTE_VALUE. Puede determinar exactamente para qué atributo de entrada es el coeficiente utilizando el identificador de nodo en la columna ATTRIBUTE_NAME. Por ejemplo, el identificador de nodo 6000000000000000a hace referencia el atributo de entrada y al valor, `Day of Week = 'Tue.'` Puede utilizar el identificador de nodo para crear una consulta o puede ir al nodo utilizando el [Visor de árbol de contenido genérico de Microsoft](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).  
  
 De igual forma, si consulta la tabla NODE_DISTRIBUTION de los nodos del nivel de salida (NODE_TYPE = 23), puede ver los coeficientes de cada valor de salida. Sin embargo, en el nivel de salida, los punteros hacen referencia a los nodos del nivel oculto. Para más información, vea [Contenido del modelo de minería de datos para los modelos de red neuronal &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
## <a name="using-a-neural-network-model-to-make-predictions"></a>Utilizar un modelo de red neuronal para realizar predicciones  
 El algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] admite tanto la clasificación como la regresión. Puede utilizar funciones de predicción con estos modelos para proporcionar datos nuevos y crear predicciones singleton o por lotes.  
  
###  <a name="bkmk_Query5"></a> Consulta de ejemplo 5: crear una predicción singleton  
 La manera más fácil de generar una consulta de predicción en un modelo de red neuronal es utilizar el Generador de consultas de predicción, disponible en la pestaña **Predicción de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Puede examinar el modelo en el Visor de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] para filtrar los atributos de interés y las tendencias de vista, y a continuación cambiar a la pestaña **Predicción de minería de datos** para crear una consulta y predecir los valores nuevos para esas tendencias.  
  
 Por ejemplo, puede examinar el modelo de centro de atención telefónica para ver las correlaciones entre los volúmenes de pedidos y otros atributos. Para ello, abra el modelo en el Visor y para **entrada**, seleccione  **\<todos >**.  Después, como **Salida**, seleccione **Number of Orders**. Como **Valor 1**, seleccione el intervalo que representa la mayoría de los pedidos y como **Valor 2**, seleccione el intervalo que representa los pedidos menores. A continuación, puede ver de un vistazo todos los atributos que el modelo pone en correlación con el volumen de pedidos.  
  
 Al examinar los resultados en el visor, puede ver que ciertos días de la semana tienen los menores volúmenes de pedidos y que un aumento en el número de operadores parece estar correlacionado con ventas mayores. Después, podría utilizar una consulta de predicción en el modelo para probar una hipótesis "qué sucedería si" y preguntar si al aumentar el número de operadores de nivel 2 en un día de volumen bajo, aumentarían los pedidos. Para ello, cree una consulta como la siguiente:  
  
```  
SELECT Predict([Call Center Default NN].[Number of Orders]) AS [Predicted Orders],  
PredictProbability([Call Center Default NN].[Number of Orders]) AS [Probability]  
FROM [Call Center Default NN]  
NATURAL PREDICTION JOIN   
(SELECT 'Tue.' AS [Day of Week],  
13 AS [Level 2 Operators]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Pedidos predichos|Probabilidad|  
|----------------------|-----------------|  
|364|0.9532…|  
  
 El volumen de ventas predicho es mayor que el intervalo actual de ventas del martes y la probabilidad de predicción es muy alta. Sin embargo, podría ser conveniente crear varias predicciones utilizando un proceso por lotes para probar una variedad de hipótesis en el modelo.  
  
> [!NOTE]  
>  Los Complementos de minería de datos para Excel 2007 ofrecen asistentes de regresión logística que facilitan el poder responder a cuestiones complejas, como cuántos operadores de nivel dos se necesitarían para mejorar el grado de servicio a un nivel determinado para un turno concreto. Los complementos de minería de datos se pueden descargar de forma gratuita e incluyen asistentes que se basan en los algoritmos de red neuronal y/o de regresión logística. Para más información, vea el sitio web [Data Mining Add-ins for Office 2007](http://go.microsoft.com/fwlink/?LinkID=117790) (Complementos de minería de datos para Office 2007).  
  
## <a name="list-of-prediction-functions"></a>Lista de funciones de predicción  
 Todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] son compatibles con un conjunto común de funciones. No hay ninguna función de predicción que sea específica del algoritmo de red neuronal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ; sin embargo, el algoritmo admite las funciones que se mencionan en la tabla siguiente.  
  
|||  
|-|-|  
|función de predicción|Uso|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|Determina si un nodo es un elemento secundario de otro nodo en el gráfico de red neuronal.|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|Devuelve la probabilidad ponderada.|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|Devuelve una tabla de valores relacionados con el valor de predicción actual.|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|Devuelve la varianza del valor de predicción.|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|Devuelve la probabilidad del valor de predicción.|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|Devuelve la desviación estándar del valor predicho.|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|En los modelos de regresión logística y de red neuronal, devuelve un valor único que representa el tamaño del conjunto de entrenamiento para todo el modelo.|  
  
 Para obtener una lista de las funciones que son comunes a todos los algoritmos de [!INCLUDE[msCoName](../../includes/msconame-md.md)], vea [Referencia de algoritmo (Analysis Services - Minería de datos)](https://technet.microsoft.com/library/bb895228\(v=sql.105\).aspx). Para obtener la sintaxis de funciones concretas, vea [Referencia de funciones de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-function-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de red neuronal de Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Referencia técnica del algoritmo de red neuronal de Microsoft](../../analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [Contenido del modelo de minería de datos para los modelos de red neuronal &#40; Analysis Services: minería de datos &#41;](../../analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [Lección 5: Generar neuronal red y los modelos de regresión logística &#40; Tutorial de minería de datos intermedios &#41;](http://msdn.microsoft.com/library/42c3701a-1fd2-44ff-b7de-377345bbbd6b)  
  
  
