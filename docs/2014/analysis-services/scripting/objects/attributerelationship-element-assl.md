---
title: Elemento AttributeRelationship (ASSL) | Microsoft Docs
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
- AttributeRelationship Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MemberProperty
helpviewer_keywords:
- AttributeRelationship element
ms.assetid: 2e786109-b8bf-4295-b0fe-9c1997349993
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a13dcac8fd37e16e90888e904cc6f0ae3587c8b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310705"
---
# <a name="attributerelationship-element-assl"></a>Elemento AttributeRelationship (ASSL)
  Proporciona detalles sobre la relación entre dos atributos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeRelationships>  
      <AttributeRelationship>  
      <AttributeID>...</AttributeID>  
            <RelationshipType>...</RelationshipType>  
      <Cardinality>...</Cardinality>  
      <Optionality >...</Optionality>  
      <OverrideBehavior >...</OverrideBehavior>  
            <Annotations>...</Annotations>  
      <Name>...</Name>  
      <Visible>...</Visible>  
      <Translations>...</Translations>  
   </AttributeRelationship>  
</AttributeRelationships>  
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
|Elementos primarios|[AttributeRelationships](../collections/relationships-element-assl.md)|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [AttributeID](../properties/id-element-assl.md), [cardinalidad](../properties/cardinality-element-assl.md), [nombre](../properties/name-element-assl.md), [opcionalidad](../properties/optionality-element-assl.md), [OverrideBehavior ](../properties/overridebehavior-element-assl.md), [RelationshipType](../properties/relationshiptype-element-assl.md), [traducciones](../collections/translations-element-assl.md), [Visible](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AttributeRelationship>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
