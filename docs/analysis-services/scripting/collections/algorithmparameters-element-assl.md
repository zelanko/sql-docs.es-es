---
title: Elemento AlgorithmParameters (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7444fd5cd5792a2e5b8ee6bfbd74eddf343d0900
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="algorithmparameters-element-assl"></a>Elemento AlgorithmParameters (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la colección de parámetros para el algoritmo usado por un [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModel>  
   ...  
   <AlgorithmParameters>  
      <AlgorithmParameter>...</AlgorithmParameter>  
   </AlgorithmParameters>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno (colección)|  
|Valor predeterminado|Ninguno (colección)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)|  
|Elementos secundarios|[AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 La colección **AlgorithmParameters** contiene un conjunto extensible de parámetros, representado como pares nombre/valor, para un algoritmo de modelo de minería de datos. El conjunto de parámetros aplicables depende del algoritmo. Para obtener más información acerca de los parámetros de algoritmo para un algoritmo dado, vea la documentación adecuada para ese algoritmo.  
  
 Los parámetros de algoritmos disponibles, incluyendo la validación y la información que se muestra, se pueden recuperar del conjunto de filas de esquema DMSCHEMA_MINING_SERVICE_PARAMETERS.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AlgorithmParameterCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Algorithm &#40;ASSL&#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)   
 [Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)   
 [Colecciones de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
