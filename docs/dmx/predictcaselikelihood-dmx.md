---
description: PredictCaseLikelihood (DMX)
title: PredictCaseLikelihood (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a08ec4809b281205386abad429afe339e0dbb1d1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727716"
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Esta función devuelve la probabilidad de que un caso de entrada vaya a caber en el modelo existente. Se utiliza solo con modelos de agrupación en clústeres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictCaseLikelihood([NORMALIZED|NONNORMALIZED])  
```  
  
## <a name="arguments"></a>Argumentos  
 NORMALIZED  
 El valor devuelto contiene la probabilidad del caso dentro modelo dividida por la probabilidad del caso sin el modelo.  
  
 NONNORMALIZED  
 El valor devuelto contiene la probabilidad sin procesar del caso, que es el producto de las probabilidades de los atributos del caso.  
  
## <a name="applies-to"></a>Se aplica a  
 Modelos compilados con los algoritmos de agrupación en clústeres [!INCLUDE[msCoName](../includes/msconame-md.md)] y [!INCLUDE[msCoName](../includes/msconame-md.md)] agrupación en clústeres de secuencia.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Número de punto flotante de doble precisión entre 0 y 1. Un número más cercano a 1 indica que el caso tiene mayor probabilidad de producirse en este modelo. Un número más cercano a 0 indica que es menos probable que se produzca el caso en este modelo.  
  
## <a name="remarks"></a>Observaciones  
 De forma predeterminada, se normaliza el resultado de la función **PredictCaseLikelihood** . Los valores normalizados son generalmente más útiles cuando aumenta el número de atributos de un caso y las diferencias entre las probabilidades sin procesar de dos casos cualesquiera se hacen mucho menores.  
  
 La ecuación siguiente se utiliza para calcular los valores normalizados a partir de los valores de x e y dados:  
  
-   x = probabilidad del caso basada en el modelo de agrupación en clústeres  
  
-   y = probabilidad marginal del caso, calculada como el logaritmo de la probabilidad del caso basada en contar los casos de entrenamiento  
  
-   Z = exp (log (x)-log (Y))  
  
 Normalizado = (z/(1 + z))  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la probabilidad de que el caso especificado se produzca dentro del modelo de agrupación en clústeres, que se basa en la base de datos [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] de DW.  
  
```  
SELECT  
  PredictCaseLikelihood() AS Default_Likelihood,  
  PredictCaseLikelihood(NORMALIZED) AS Normalized_Likelihood,  
  PredictCaseLikelihood(NONNORMALIZED) AS Raw_Likelihood,  
FROM  
  [TM Clustering]  
NATURAL PREDICTION JOIN  
(SELECT 28 AS [Age],  
  '2-5 Miles' AS [Commute Distance],  
  'Graduate Degree' AS [Education],  
  0 AS [Number Cars Owned],  
  0 AS [Number Children At Home]) AS t  
```  
  
 Resultados esperados:  
  
|Default_Likelihood|Normalized_Likelihood|Raw_Likelihood|  
|-------------------------|----------------------------|---------------------|  
|6,30672792729321E-08|6,30672792729321E-08|9,5824454056846E-48|  
  
 La diferencia entre estos resultados demuestra el efecto de la normalización. El valor sin formato de **CaseLikelihood** sugiere que la probabilidad del caso es aproximadamente el 20 por ciento; sin embargo, cuando se normalizan los resultados, se hace evidente que la probabilidad del caso es muy baja.  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos ](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
