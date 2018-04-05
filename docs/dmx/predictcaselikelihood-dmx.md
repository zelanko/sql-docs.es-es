---
title: PredictCaseLikelihood (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictCaseLikelihood
dev_langs:
- DMX
helpviewer_keywords:
- PredictCaseLikelihood function
ms.assetid: b00180e5-b2eb-49e2-891d-e39fb378f50a
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f7eb644b085cbc5686a91988fc98ada9ee2257ab
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="predictcaselikelihood-dmx"></a>PredictCaseLikelihood (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Los modelos generados mediante la [!INCLUDE[msCoName](../includes/msconame-md.md)] clústeres y [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de clústeres de secuencia.  
  
## <a name="return-type"></a>Tipo devuelto  
 Número de punto flotante de doble precisión entre 0 y 1. Un número más cercano a 1 indica que el caso tiene mayor probabilidad de producirse en este modelo. Un número más cercano a 0 indica que es menos probable que se produzca el caso en este modelo.  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, el resultado de la **PredictCaseLikelihood** se normaliza la función. Los valores normalizados son generalmente más útiles cuando aumenta el número de atributos de un caso y las diferencias entre las probabilidades sin procesar de dos casos cualesquiera se hacen mucho menores.  
  
 La ecuación siguiente se utiliza para calcular los valores normalizados a partir de los valores de x e y dados:  
  
-   x = probabilidad del caso basada en el modelo de agrupación en clústeres  
  
-   y = probabilidad marginal del caso, calculada como el logaritmo de la probabilidad del caso basada en contar los casos de entrenamiento  
  
-   Z = Exp( log(x) – Log(Y))  
  
 Normaliza = (z / (1 + z))  
  
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
  
 La diferencia entre estos resultados demuestra el efecto de la normalización. El valor sin formato de **CaseLikelihood** sugiere que la probabilidad del caso es aproximadamente un 20 por ciento; sin embargo, al normalizar los resultados, es evidente que la probabilidad del caso es muy baja.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40; Analysis Services: minería de datos &#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
