---
title: Elemento KeyColumn (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e22b3b5872ce75f7b93ce334df2d4214df176eb0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="keycolumn-element-assl"></a>Elemento KeyColumn (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Contiene la definición de una columna que es o forma parte de la clave de un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<KeyColumns>  
   <KeyColumn xsi:type="DataItem">...</KeyColumn>  
<KeyColumns>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[Elemento de datos](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información sobre la **DataItem** tipo, incluida una tabla de objetos de Analysis Services Scripting Language (ASSL) y las propiedades de la **DataItem** los tipos, vea [tipo de datos de elemento de datos & #40; ASSL & #41; ](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md).  
  
 Los elementos que corresponden a los elementos primarios de la **KeyColumns** colección en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.AggregationInstanceAttribute>, <xref:Microsoft.AnalysisServices.DimensionAttribute>, <xref:Microsoft.AnalysisServices.MeasureGroupAttribute>, y <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos AggregationInstanceAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstanceattribute-data-type-assl.md)   
 [Tipo de datos AggregationInstanceCubeDimension &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/aggregationinstancecubedimension-data-type-assl.md)   
 [Tipo de datos DimensionAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)   
 [Tipo de datos MeasureGroupAttribute &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/measuregroupattribute-data-type-assl.md)   
 [Tipo de datos ScalarMiningStructureColumn &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)   
 [Objetos de & #40; ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
