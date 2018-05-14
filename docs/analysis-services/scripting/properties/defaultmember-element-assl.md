---
title: Elemento DefaultMember (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: aad56fe9918235afb24a8f8f56bf98715964125a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="defaultmember-element-assl"></a>Elemento DefaultMember (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene una expresión MDX (Expresiones multidimensionales) que identifica el miembro predeterminado del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributePermission> <!-- or DimensionAttribute, ManyToManyMeasureGroupDimension, PerspectiveAttribute -->  
      ...  
   <DefaultMember>...</DefaultMember>  
      ...  
</AttributePermission>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[AttributePermission](../../../analysis-services/scripting/objects/attributepermission-element-assl.md), [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md), [ManyToManyMeasureGroupDimension](../../../analysis-services/scripting/data-type/manytomanymeasuregroupdimension-data-type-assl.md), [PerspectiveAttribute](../../../analysis-services/scripting/data-type/perspectiveattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **DefaultMember** define el miembro predeterminado del elemento primario. Si **DefaultMember** no se especifica o se establece en una cadena vacía, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] elige un miembro que se usará como el miembro predeterminado.  
  
 Para los elementos **ManyToManyMeasureGroupDimension** , el elemento **DefaultMember** contiene una expresión MDX que especifica un miembro en la dimensión identificada en el elemento **CubeDimensionID** de **ManyToManyMeasureGroupDimension**. La expresión MDX es similar a la [StrToMember](../../../mdx/strtomember-mdx.md) función MDX con la palabra clave CONSTRAINED, en que no puede incluir MDX o funciones definidas por el usuario.  
  
 Para más información sobre los miembros predeterminados, vea [Definir un miembro predeterminado](../../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
 Los elementos que corresponden a los elementos primarios de **DefaultMember** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AttributePermission>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, y <xref:Microsoft.AnalysisServices.PerspectiveAttribute>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
