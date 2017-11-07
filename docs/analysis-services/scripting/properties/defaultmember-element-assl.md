---
title: Elemento DefaultMember (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DefaultMember Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DefaultMember
helpviewer_keywords:
- DefaultMember element
ms.assetid: db4eea9f-f7cf-40de-abd0-b62014e7ec2d
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 411fbf97001ee719e144edfdd6de685e984da021
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

