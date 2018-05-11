---
title: Elemento RelationshipType (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d740a3bed4b9fe8d9aa3bf259a9b83a59af26f5a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="relationshiptype-element-assl"></a>Elemento RelationshipType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Indica si las relaciones de miembros para un [AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md) puede cambiarse.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <RelationshipType>...</RelationshipType>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Flexible*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributeRelationship](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Rígida*|Las relaciones de miembro entre un atributo y un atributo relacionado no se pueden cambiar.|  
|*Flexible*|Las relaciones de miembro entre un atributo y un atributo relacionado se pueden cambiar.|  
  
 Por ejemplo, si **ZipCode** no puede cambiar de un **City** a otro, la relación de **ZipCode** a **City** se marca como *Rigid*.  
  
 La enumeración que corresponde a los valores permitidos para **RelationshipType** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.RelationshipType>.  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributo](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
