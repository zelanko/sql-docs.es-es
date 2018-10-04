---
title: Elemento IntermediateGranularityAttributeID (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- IntermediateGranularityAttributeID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- IntermediateGranularityAttributeID
helpviewer_keywords:
- IntermediateGranularityAttributeID element
ms.assetid: 49895ff0-cb0d-4bcc-ab73-8cb3d5961e12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b225cffc90de044e2ea5d46a8e53091240d834a0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091045"
---
# <a name="intermediategranularityattributeid-element-assl"></a>Elemento IntermediateGranularityAttributeID (ASSL)
  Contiene el identificador (Id.) del atributo de granularidad en la dimensión del cubo intermedia que se utiliza para relacionar una dimensión de referencia con una dimensión intermedia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ReferenceMeasureGroupDimension>  
   ...  
   <IntermediateGranularityAttributeID>...  
   </IntermediateGranularityAttributeID>  
   ...  
</ReferenceMeasureGroupDimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ReferenceMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `IntermediateGranularityAttributeID` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
