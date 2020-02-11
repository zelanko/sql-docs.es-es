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
ms.openlocfilehash: 523c57811ca29956edc3c18b8143844732c163b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892395"
---
# <a name="clusterdistance-dmx"></a>ClusterDistance (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La función **ClusterDistance** devuelve la distancia del caso de entrada del clúster especificado o, si no se especifica ningún clúster, la distancia del caso de entrada del clúster más probable.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ClusterDistance([<ClusterID expression>])  
```  
  
## <a name="applies-to"></a>Se aplica a  
 Esta función solo se puede utilizar si el modelo de minería de datos subyacente admite la agrupación en clústeres. La función se puede utilizar con cualquier tipo de modelo de agrupación en clústeres (EM, mediana-K, etc.), pero los resultados difieren según el algoritmo.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 La función **ClusterDistance** devuelve la distancia entre el caso de entrada y el clúster que tiene la probabilidad más alta para ese caso de entrada.  
  
 En el caso de la agrupación en clústeres mediana-K, dado que cualquier caso puede pertenecer a un único clúster, con un peso de pertenencia de 1.0, la distancia del clúster siempre es 0. Sin embargo, se supone que con mediana-K, cada clúster tiene un centroide. Puede obtener el valor del centroide consultando o examinando la tabla anidada NODE_DISTRIBUTION en el contenido del modelo de minería de datos. Para obtener más información, vea [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining).  
  
 En el caso del método de agrupación en clústeres EM predeterminado, todos los puntos dentro del clúster se consideran igualmente probables; por consiguiente, por diseño no hay centroide para el clúster. El valor de **ClusterDistance** entre un caso determinado y un clúster *N* determinado se calcula de la manera siguiente:  
  
 ClusterDistance (N) = 1-(membershipWeight (N))  
  
 O bien:  
  
 ClusterDistance (N) = 1-ClusterProbability (N))  
  
## <a name="related-prediction-functions"></a>Funciones de predicción relacionadas  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona las funciones adicionales siguientes para consultar los modelos de agrupación en clústeres:  
  
-   Use la función [cluster &#40;DMX&#41;](../dmx/cluster-dmx.md) para devolver el clúster más probable.  
  
-   Use la función [ClusterProbability &#40;DMX&#41;](../dmx/clusterprobability-dmx.md) para obtener la probabilidad de que un caso pertenezca a un clúster determinado. Este valor actúa como la inversa de la distancia del clúster.  
  
-   Use la función [PredictHistogram &#40;DMX&#41;](../dmx/predicthistogram-dmx.md) para devolver un histograma de la probabilidad del caso de entrada existente en cada uno de los clústeres del modelo.  
  
-   Use la función [PredictCaseLikelihood &#40;DMX&#41;](../dmx/predictcaselikelihood-dmx.md) para devolver una medida de 0 a 1 que indique la probabilidad de que exista un caso de entrada en el modelo aprendido por el algoritmo.  
  
## <a name="example1-obtaining-cluster-distance-to-the-most-likely-cluster"></a>Ejemplo 1: obtener la distancia de clúster para el clúster más probable  
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
  
 Resultados de ejemplo:  
  
|Expression|  
|----------------|  
|0.0477390930705145|  
  
 Para averiguar qué clúster es este, puede sustituir `Cluster` por `ClusterDistance` en el ejemplo anterior.  
  
 Resultados de ejemplo:  
  
|$CLUSTER|  
|--------------|  
|Clúster 6|  
  
## <a name="example2-obtaining-distance-to-a-specified-cluster"></a>Ejemplo 2: obtener la distancia a un clúster especificado  
 La siguiente sintaxis usa el conjunto de filas de esquema del contenido del modelo de minería de datos para devolver la lista de identificadores de nodo y títulos de nodo para los clústeres que existen en el modelo de minería de datos. Después, puede usar el título del nodo como el argumento del identificador de clúster en la función **ClusterDistance** .  
  
```  
SELECT NODE_UNIQUE_NAME, NODE_CAPTION   
FROM <model>.CONTENT   
WHERE NODE_TYPE = 5  
```  
  
 Resultados de ejemplo:  
  
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
  
 Resultados de ejemplo:  
  
|Cluster 2 Distance|  
|------------------------|  
|0.97008209236394|  
  
## <a name="see-also"></a>Consulte también  
 [&#41;de &#40;DMX de clúster](../dmx/cluster-dmx.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services-Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-clustering-models-analysis-services-data-mining)  
  
  
