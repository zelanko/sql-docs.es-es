---
title: Elemento optionality (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Optionality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Optionality element
ms.assetid: 6cd2ef0a-6fbe-4462-ab27-4cdfeb33f8ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d59b04dad688d438ca2f4777b404dcc4fe8976b1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099175"
---
# <a name="optionality-element-assl"></a>Elemento Optionality (ASSL)
  Indica la opcionalidad de los miembros de un [AttributeRelationship](../objects/attributerelationship-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeRelationship>  
   ...  
   <Optionality>...</OPtionality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*obligatorio*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributeRelationship](../objects/attributerelationship-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*obligatorio*|Cada miembro en el atributo relacionado tiene que estar asociado por lo menos a un miembro en el atributo al que pertenece el elemento `AttributeRelationship`.|  
|*Opcional*|Cada miembro en el atributo relacionado no tiene que estar asociado por lo menos a un miembro en el atributo al que pertenece el elemento `AttributeRelationship`.|  
  
 La enumeración que corresponde a los valores permitidos para `Cardinality` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Optionality>.  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributo](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
