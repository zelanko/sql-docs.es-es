---
title: ClusterDistance (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1884bf191d842ba136165cf28aa14c23dd82b2e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071072"
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  El **ClusterDistance** función devuelve la distancia del caso de entrada desde el clúster especificado, o si no se especifica ningún clúster, la distancia del caso de entrada desde el clúster más probable.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Esta función solo se puede utilizar si el modelo de minería de datos subyacente admite la agrupación en clústeres. La función se puede utilizar con cualquier tipo de modelo de agrupación en clústeres (EM, mediana-K, etc.), pero los resultados difieren según el algoritmo.  
  
## <a name="return-type"></a>Tipo devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 El **ClusterDistance** función devuelve la distancia entre el caso de entrada y el clúster que tiene la mayor probabilidad de que el caso de entrada.  
  
 En el caso de la agrupación en clústeres mediana-K, dado que cualquier caso puede pertenecer a un único clúster, con un peso de pertenencia de 1.0, la distancia del clúster siempre es 0. Sin embargo, se supone que con mediana-K, cada clúster tiene un centroide. Puede obtener el valor del centroide consultando o examinando la tabla anidada NODE_DISTRIBUTION en el contenido del modelo de minería de datos. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md).  
  
 En el caso del método de agrupación en clústeres EM predeterminado, todos los puntos dentro del clúster se consideran igualmente probables; por consiguiente, por diseño no hay centroide para el clúster. El valor de **ClusterDistance** entre un caso determinado y un clúster determinado *N* se calcula como sigue:  
  
 ClusterDistance(N) =1-(membershipWeight(N))  
  
 O:  
  
 ClusterDistance(N) = 1-ClusterProbability (N))  
  
## <a name="related-prediction-functions"></a>Funciones de predicción relacionadas  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona las funciones adicionales siguientes para consultar los modelos de agrupación en clústeres:  
  
-   Use la [clúster &#40;DMX&#41; ](../dmx/cluster-dmx.md) función para devolver el clúster más probable.  
  
-   Use la [ClusterProbability &#40;DMX&#41; ](../dmx/clusterprobability-dmx.md) función para obtener la probabilidad de que un caso pertenezca a un clúster determinado. Este valor actúa como la inversa de la distancia del clúster.  
  
-   Use la [PredictHistogram &#40;DMX&#41; ](../dmx/predicthistogram-dmx.md) función para devolver un histograma de la probabilidad de que la entrada existente case en cada uno de los clústeres del modelo.  
  
-   Use la [PredictCaseLikelihood &#40;DMX&#41; ](../dmx/predictcaselikelihood-dmx.md) función para devolver una medida de 0 a 1 que indica la probabilidad de que un caso de entrada es que exista teniendo en cuenta el modelo aprendido por el algoritmo.  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>Ejemplo 1: Obtener la distancia del clúster al clúster más probable  
 En el ejemplo siguiente se devuelve la distancia del caso especificado para el clúster al que es más probable que el caso pertenezca.  
  
```  
SELECT  
    ClusterDistance()  
FROM  
    [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Expresión|  
|----------------|  
|0.0477390930705145|  
  
 Para averiguar qué clúster es este, puede sustituir `Cluster` por `ClusterDistance` en el ejemplo anterior.  
  
 Resultados del ejemplo:  
  
|$CLUSTER|  
|--------------|  
|Clúster 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>Ejemplo 2: Obtener la distancia a un clúster especificado  
 La siguiente sintaxis usa el conjunto de filas de esquema del contenido del modelo de minería de datos para devolver la lista de identificadores de nodo y títulos de nodo para los clústeres que existen en el modelo de minería de datos. A continuación, puede usar la leyenda del nodo como el argumento de identificador de clúster en el **ClusterDistance** función.  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 Resultados del ejemplo:  
  
|NODE_UNIQUE_NAME|NODE_CAPTION|  
|------------------------|-------------------|  
|001|Clúster 1|  
|002|Clúster 2|  
  
 El ejemplo de sintaxis siguiente devuelve la distancia del caso especificado desde el clúster con la etiqueta Cluster 2.  
  
```  
SELECT  
    ClusterDistance('Cluster 2')  
AS [Cluster 2 Distance]  
FROM [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
    '2-5 Miles' AS [Commute Distance],  
    'Graduate Degree' AS [Education],  
    0 AS [Number Cars Owned],  
    0 AS [Number Children At Home]) AS t  
```  
  
 Resultados del ejemplo:  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>Vea también  
 [Clúster &#40;DMX&#41;](../dmx/cluster-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
