---
title: Elemento EstimatedCount (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EstimatedCount Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EstimatedCount
helpviewer_keywords:
- EstimatedCount element
ms.assetid: ce84b54a-8ab2-42f4-a7dd-e10a3d41cb4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc65def1576c28a9a21249501f83986c2652652d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155721"
---
# <a name="estimatedcount-element-assl"></a>Elemento EstimatedCount (ASSL)
  Contiene el número estimado de miembros para un atributo, definido por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AggregationDesignAttribute> <!-- or DimensionAttribute -->  
      ...  
   <EstimatedCount>...</EstimatedCount>  
   ...  
</AggregationDesignAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Long|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[AggregationDesignAttribute](../data-type/aggregationdesignattribute-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Este valor se asigna por el usuario y está usando el [elemento AggregationDesign &#40;ASSL&#41;](../objects/aggregationdesign-element-assl.md).  
  
 Los elementos que corresponden a los elementos primarios de `EstimatedCount` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AggregationDesignAttribute> y <xref:Microsoft.AnalysisServices.DimensionAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
