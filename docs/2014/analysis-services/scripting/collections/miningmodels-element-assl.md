---
title: Elemento MiningModels (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MiningModels Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModels
helpviewer_keywords:
- MiningModels element
ms.assetid: 19824d92-2e23-4e5e-b329-e46baf709c4a
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e1901ff4974104143928c9b5fb90d14118fda6a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291611"
---
# <a name="miningmodels-element-assl"></a>Elemento MiningModels (ASSL)
  Contiene la colección de [MiningModel](../objects/miningmodel-element-assl.md) elementos asociados con un [MiningStructure](../objects/miningstructure-element-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningStructure>  
   ...  
   <MiningModels>  
      <MiningModel>...</MiningModel>  
   </MiningModels>  
   ...  
</MiningStructure>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[MiningStructure](../objects/miningstructure-element-assl.md)|  
|Elementos secundarios|[MiningModel](../objects/miningmodel-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.MiningModelCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
