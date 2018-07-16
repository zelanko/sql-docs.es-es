---
title: Elemento IsKey (ASSL) | Microsoft Docs
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
- IsKey Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IsKey
helpviewer_keywords:
- IsKey element
ms.assetid: 523b26c8-5cce-415d-a360-9a0d8724b872
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 755d401f304b04e675f343911ef127050552b789
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288031"
---
# <a name="iskey-element-assl"></a>Elemento IsKey (ASSL)
  Indica si la columna proporciona la clave para el caso en un [MiningStructure](../objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <IsKey>...</IsKey>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Se puede designar una o más columnas como columnas de clave para cada nivel de una estructura de tabla anidada.  
  
 El elemento que se corresponde con el elemento primario de `IsKey` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
