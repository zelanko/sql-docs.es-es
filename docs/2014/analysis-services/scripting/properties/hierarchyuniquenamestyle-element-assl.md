---
title: Elemento HierarchyUniqueNameStyle (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- HierarchyUniqueNameStyle Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- HierarchyUniqueNameStyle element
ms.assetid: 2ac57825-e9e5-4ec4-9856-fa2326d2c43f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04776eb3c9f20e0fa8c870621020c466ba625826
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196875"
---
# <a name="hierarchyuniquenamestyle-element-assl"></a>Elemento HierarchyUniqueNameStyle (ASSL)
  Determina los nombres únicos de cómo se generan para las jerarquías contenidas en el [CubeDimension](../data-type/dimension-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CubeDimension>  
   ...  
   <HierarchyUniqueNameStyle>...</HierarchyUniqueNameStyle>  
   ...  
</CubeDimension>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*IncludeDimensionName*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[CubeDimension](../data-type/dimension-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*IncludeDimensionName*|El nombre de la dimensión se incluye como parte del nombre de la jerarquía.|  
|*ExcludeDimensionName*|El nombre de la dimensión no se incluye como parte del nombre de la jerarquía.|  
  
 El elemento que se corresponde con el elemento primario de `HierarchyUniqueNameStyle` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.CubeDimension>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento de dimensión &#40;ASSL&#41;](../objects/dimension-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
