---
title: Elemento DefaultMember (ASSL) | Microsoft Docs
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
- DefaultMember Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fd074ab38264bf45ad70a96c37a22bc3c3185d4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229685"
---
# <a name="defaultmember-element-assl"></a>Elemento DefaultMember (ASSL)
  Contiene una expresión MDX (Expresiones multidimensionales) que identifica el miembro predeterminado del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributePermission](../objects/attributepermission-element-assl.md), [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md), [ManyToManyMeasureGroupDimension](../data-type/dimension-data-type-assl.md), [PerspectiveAttribute](../data-type/perspectiveattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `DefaultMember` define el miembro predeterminado del elemento primario. Si `DefaultMember` no se especifica o se establece en una cadena vacía, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] elige un miembro que se usará como el miembro predeterminado.  
  
 Para los elementos `ManyToManyMeasureGroupDimension`, el elemento `DefaultMember` contiene una expresión MDX que especifica un miembro en la dimensión identificada en el elemento `CubeDimensionID` de `ManyToManyMeasureGroupDimension`. La expresión MDX es similar a la [StrToMember](/sql/mdx/strtomember-mdx) función MDX con la palabra clave CONSTRAINED, en eso no se puede incluir MDX o funciones definidas por el usuario.  
  
 Para más información sobre los miembros predeterminados, vea [Definir un miembro predeterminado](../../multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 Los elementos que corresponden a los elementos primarios de `DefaultMember` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute> y <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
