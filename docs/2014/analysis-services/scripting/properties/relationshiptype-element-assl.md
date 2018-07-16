---
title: Elemento RelationshipType (ASSL) | Microsoft Docs
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
- RelationshipType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RelationshipType
helpviewer_keywords:
- RelationshipType element
ms.assetid: 72e1ab0e-a95d-4ebe-857d-21de1bf9fe03
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21ddd4506a2c2a6168779aa40735eb7177406597
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37271601"
---
# <a name="relationshiptype-element-assl"></a>Elemento RelationshipType (ASSL)
  Indica si las relaciones de miembros para un [AttributeRelationship](../objects/attributerelationship-element-assl.md) puede cambiarse.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Flexible*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Rígido*|Las relaciones de miembro entre un atributo y un atributo relacionado no se pueden cambiar.|  
|*Flexible*|Las relaciones de miembro entre un atributo y un atributo relacionado se pueden cambiar.|  
  
 Por ejemplo, si `ZipCode` no se puede cambiar de uno `City` a otro, la relación de `ZipCode` a `City` está marcado como *rígida*.  
  
 La enumeración que corresponde a los valores permitidos para `RelationshipType` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.RelationshipType>.  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributo](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
