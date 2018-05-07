---
title: Elemento AlgorithmParameter (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea1756e291ff5e41b7d22dac0255fe448b5be06d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="algorithmparameter-element-assl"></a>Elemento AlgorithmParameter (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un parámetro para el algoritmo usado por un [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AlgorithmParameters>  
   <AlgorithmParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </AlgorithmParameter>  
</AlgorithmParameters>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AlgorithmParameters](../../../analysis-services/scripting/collections/algorithmparameters-element-assl.md)|  
|Elementos secundarios|[Name](../../../analysis-services/scripting/properties/name-element-assl.md), [Value](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 **AlgorithmParameter** es un parámetro para un algoritmo del modelo de minería de datos. **AlgorithmParameter** representa este parámetro como un par de nombre/valor. El conjunto de parámetros aplicables que **AlgorithmParameter** puede representar es depende del algoritmo. Para obtener más información acerca de los parámetros de algoritmo para un algoritmo dado, vea la documentación adecuada para ese algoritmo.  
  
 Parámetros de algoritmos disponibles, incluida la información de validación y presentación, se pueden recuperar desde el [DMSCHEMA_MINING_SERVICE_PARAMETERS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md) de filas de esquema.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AlgorithmParameter>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento MiningModel &#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [Elemento Algorithm &#40;ASSL&#41;](../../../analysis-services/scripting/properties/algorithm-element-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
