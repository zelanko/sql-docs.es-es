---
title: Elemento Cardinality (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cardinality Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Cardinality element
ms.assetid: 60ac8a26-7c8b-4011-9b9b-a29863779428
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b90e85efbde384bd0d2854fdb2bbd4b325632e2d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197259"
---
# <a name="cardinality-element-assl"></a>Elemento Cardinality (ASSL)
  Indica la cardinalidad de la relación descrita por un [AttributeRelationship](../objects/attributerelationship-element-assl.md) o [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeRelationship> <!-- or RegularMeasureGroupDimension -->  
   ...  
   <Cardinality>...</Cardinality>  
   ...  
</AttributeRelationship>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Muchos*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributeRelationship](../objects/attributerelationship-element-assl.md), [RegularMeasureGroupDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Muchos*|Relación de varios a uno|  
|*Uno*|Relación de uno a uno|  
  
 La enumeración que corresponde a los valores permitidos de `Cardinality` en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.Cardinality>.  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributo](../../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  