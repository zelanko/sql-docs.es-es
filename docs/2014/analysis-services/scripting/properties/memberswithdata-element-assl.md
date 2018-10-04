---
title: Elemento MembersWithData (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MembersWithData Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MembersWithData
helpviewer_keywords:
- MembersWithData element
ms.assetid: 845087a2-b12d-4344-a8be-85ca61155296
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 17a3fced7327c1fb2211b1c80f774ae859757952
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48089659"
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
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El valor de la `MembersWithData` elemento es utilizado únicamente por los atributos primarios (en otras palabras, el valor de la [uso](usage-element-dimensionattribute-assl.md) elemento de la `DimensionAttribute` elemento primario se establece en *primario*) para determinar si para mostrar a los miembros de datos para los miembros no hoja del atributo primario. Para obtener más información sobre los miembros de datos, vea [Atributos en las jerarquías de elementos primarios y secundarios](../../multidimensional-models/parent-child-dimension-attributes.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*NonLeafDataHidden*|Se ocultan los datos no hoja.|  
|*NonLeafDataVisible*|Los datos no hoja son visibles.|  
  
 La enumeración que corresponde a los valores permitidos para `MembersWithData` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MembersWithData>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento MembersWithDataCaption &#40;ASSL&#41;](caption-element-assl.md)   
 [Tipo de datos DimensionAttribute &#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
