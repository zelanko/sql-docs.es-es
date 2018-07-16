---
title: Elemento AlgorithmParameter (ASSL) | Microsoft Docs
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
- AlgorithmParameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AlgorithmParameter
helpviewer_keywords:
- AlgorithmParameter element
ms.assetid: 73211495-065c-43c6-a486-be6044617263
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd5ee9ceb1c8d2455d7e9c087e12e2f59625b5ab
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178862"
---
# <a name="algorithmparameter-element-assl"></a>Elemento AlgorithmParameter (ASSL)
  Define un parámetro para el algoritmo utilizado por un [MiningModel](miningmodel-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AlgorithmParameters>  
   <AlgorithmParameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </AlgorithmParameter>  
</AlgorithmParameters>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AlgorithmParameters](../collections/algorithmparameters-element-assl.md)|  
|Elementos secundarios|[Name](../properties/name-element-assl.md), [Value](../properties/value-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 `AlgorithmParameter` es un parámetro para un algoritmo del modelo de minería de datos. `AlgorithmParameter` representa este parámetro como un par de nombre/valor. El conjunto de parámetros aplicables que `AlgorithmParameter` puede representar es depende del algoritmo. Para obtener más información acerca de los parámetros de algoritmo para un algoritmo dado, vea la documentación adecuada para ese algoritmo.  
  
 Parámetros de algoritmos disponibles, incluida la información de validación y presentación, se pueden recuperar desde el [DMSCHEMA_MINING_SERVICE_PARAMETERS](../../schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md) de filas de esquema.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AlgorithmParameter>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento MiningModel &#40;ASSL&#41;](miningmodel-element-assl.md)   
 [Elemento Algorithm &#40;ASSL&#41;](../properties/algorithm-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
