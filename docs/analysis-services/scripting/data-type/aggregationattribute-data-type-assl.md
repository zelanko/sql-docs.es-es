---
title: Tipo de datos AggregationAttribute (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f63f055c024d746484b5829617a0e34bee1ba5b0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="aggregationattribute-data-type-assl"></a>Tipo de datos AggregationAttribute (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo que representa la asociación existente entre un elemento [Aggregation](../../../analysis-services/scripting/objects/aggregation-element-assl.md) y un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AggregationAttribute>  
   <AttributeID>...</AttributeID>  
      <Annotations>...</Annotations>  
</AggregationAttribute>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [Annotations](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|Elementos derivados|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) (colección[Attributes](../../../analysis-services/scripting/collections/attributes-element-assl.md) de [AggregationDimension](../../../analysis-services/scripting/data-type/aggregationdimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 La clase correspondiente en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.AggregationAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Aggregation, elemento & #40; ASSL & #41;](../../../analysis-services/scripting/objects/aggregation-element-assl.md)   
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
