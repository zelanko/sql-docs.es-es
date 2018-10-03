---
title: Elemento AttributeHierarchyVisible (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AttributeHierarchyVisible Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeHierarchyVisible
helpviewer_keywords:
- AttributeHierarchyVisible element
ms.assetid: a3289a9a-dbd6-43e8-a7ca-ee8a1da92a32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac33cb91014a32f3795b10ef822ab6c85528ac0b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48099275"
---
# <a name="attributehierarchyvisible-element-assl"></a>Elemento AttributeHierarchyVisible (ASSL)
  Determina si la jerarquía de atributos es visible para las aplicaciones cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute> <!-- or CubeAttribute or PerspectiveAttribute -->  
   ...  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|`True`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[CubeAttribute](../data-type/cubeattribute-data-type-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `AttributeHierarchyVisible` determina si la jerarquía de atributos asociada al atributo está visible para las aplicaciones cliente. Aunque este elemento esté establecido en `False`, se puede usar la jerarquía de atributos para crear jerarquías de atributos definidas por el usuario y se puede hacer referencia a ella en instrucciones MDX (Expresiones multidimensionales).  
  
 Los elementos que corresponden a los elementos primarios de `AttributeHierarchyVisible` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.CubeAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute> y <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento AttributeHierarchyEnabled &#40;ASSL&#41;](enabled-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
