---
title: Elemento Algorithm (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Algorithm Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Algorithm
helpviewer_keywords:
- Algorithm element
ms.assetid: 188bf7ce-c5c9-406a-af75-5a026c92a569
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fb2ab30f6abd753f0c954ef41ad26d0af9dcda8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149785"
---
# <a name="algorithm-element-assl"></a>Elemento Algorithm (ASSL)
  Define el algoritmo utilizado por un [MiningModel](../objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel>  
      ...  
   <Algorithm>...</Algorithm>  
      ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../objects/miningmodel-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor del elemento `Algorithm` es una cadena que identifica el algoritmo. Por ejemplo, podría ser la cadena *Microsoft_Naive_Bayes*, *Microsoft_Decision_Trees*, o *Microsoft_Clustering.* La cadena identifica los algoritmos suministrados por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] y los algoritmos personalizados proporcionados por el usuario. Los valores disponibles para el `Algorithm` se puede recuperar el elemento de la columna SERVICE_NAME del [DMSCHEMA_MINING_SERVICES](../../schema-rowsets/data-mining/dmschema-mining-services-rowset.md) de filas de esquema.  
  
 El elemento que se corresponde con el elemento primario de `Algorithm` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningModel>. Un elemento estrechamente relacionado en el modelo de objetos de Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.MiningModelAlgorithms>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento AlgorithmParameter &#40;ASSL&#41;](../objects/algorithmparameter-element-assl.md)   
 [Elemento AlgorithmParameters &#40;ASSL&#41;](../collections/algorithmparameters-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
