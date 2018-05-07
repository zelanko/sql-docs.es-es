---
title: Elemento AttributeRelationships (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 222f230c1de371a30f6a82524fc769ed9dc79926
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="attributerelationships-element-assl"></a>Elemento AttributeRelationships (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la colección de [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) elementos para el atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute xsi:type="DimensionAttribute">  
   ...  
   <AttributeRelationships>  
      <AttributeRelationship>...</AttributeRelationship>  
   </AttributeRelationships>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Attribute](../../../analysis-services/scripting/objects/attribute-element-assl.md) de tipo [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AttributeRelationshipCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones de & #40; ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
