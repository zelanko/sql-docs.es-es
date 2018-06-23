---
title: Elemento AlgorithmParameters (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AlgorithmParameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AlgorithmParameters
helpviewer_keywords:
- AlgorithmParameters element
ms.assetid: 240cbb60-7fa3-46ef-b5be-cd14c9ec10de
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c73495677fd6a1eaf8ff1c70f154bf240b04e709
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201908"
---
# <a name="algorithmparameters-element-assl"></a>Elemento AlgorithmParameters (ASSL)
  Contiene la colección de parámetros para el algoritmo usado por un [MiningModel](../objects/miningmodel-element-assl.md) elemento.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno (colección)|  
|Valor predeterminado|Ninguno (colección)|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModel](../objects/miningmodel-element-assl.md)|  
|Elementos secundarios|[AlgorithmParameter](../objects/algorithmparameter-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 La colección `AlgorithmParameters` contiene un conjunto extensible de parámetros, representado como pares nombre/valor, para un algoritmo de modelo de minería de datos. El conjunto de parámetros aplicables depende del algoritmo. Para obtener más información acerca de los parámetros de algoritmo para un algoritmo dado, vea la documentación adecuada para ese algoritmo.  
  
 Los parámetros de algoritmos disponibles, incluyendo la validación y la información que se muestra, se pueden recuperar del conjunto de filas de esquema DMSCHEMA_MINING_SERVICE_PARAMETERS.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AlgorithmParameterCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Algorithm &#40;ASSL&#41;](../properties/algorithm-element-assl.md)   
 [Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS](../../schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  