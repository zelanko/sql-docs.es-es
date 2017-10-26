---
title: Elemento MembersWithData (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MembersWithData Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MembersWithData
helpviewer_keywords:
- MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e699a61dafb6f7bf9274fdf76dda5cdc0694c3dd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="memberswithdata-element-assl"></a>Elemento MembersWithData (ASSL)
  Determina si se van a mostrar los miembros de datos para los miembros no hoja del atributo primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <MembersWithData>...</MembersWithData>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*NonLeafDataVisible*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la **MembersWithData** elemento se utiliza únicamente por los atributos primarios (en otras palabras, el valor de la [uso](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) elemento de la **DimensionAttribute** elemento primario se establece en *primario*) para determinar si se debe mostrar los miembros de datos para los miembros no hoja del atributo primario. Para obtener más información sobre los miembros de datos, vea [Atributos en las jerarquías de elementos primarios y secundarios](../../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*NonLeafDataHidden*|Se ocultan los datos no hoja.|  
|*NonLeafDataVisible*|Los datos no hoja son visibles.|  
  
 La enumeración que corresponde a los valores permitidos para **MembersWithData** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MembersWithData>.  
  
## <a name="see-also"></a>Vea también  
 [Memberswithdatacaption, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/memberswithdatacaption-element-assl.md)   
 [Tipo de datos DimensionAttribute &#40; ASSL &#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

