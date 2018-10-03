---
title: Elemento OverrideBehavior (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- OverrideBehavior Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- OverrideBehavior element
ms.assetid: 6a5b361a-6061-4b73-b1a7-1237fb77606c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 88cf3dd287e1b55fee5377e2238d4d7c738cfe16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203625"
---
# <a name="overridebehavior-element-assl"></a>Elemento OverrideBehavior (ASSL)
  Indica el comportamiento de invalidación de la relación descrita por un [AttributeRelationship](../objects/attributerelationship-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <OverrideBehavior>...</OverrideBehavior>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Seguro*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `OverrideBehavior` determina cómo la posición en el atributo relacionado afecta a la posición en el atributo  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Seguro*|Indica el comportamiento de invalidación de la relación descrita por un elemento AttributeRelationship. Indica cómo la colocación en un atributo afecta a la posición del otro.|  
|*Ninguno*|Ningún efecto.|  
  
 La enumeración que corresponde a los valores permitidos para `OverrideBehavior` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.OverrideBehavior>.  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributo](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
