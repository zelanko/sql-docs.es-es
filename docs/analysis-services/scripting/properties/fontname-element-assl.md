---
title: Elemento FontName (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cc6fe14162febf9b3655876bfaad25505ce07079
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031696"
---
# <a name="fontname-element-assl"></a>Elemento FontName (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe las características de presentación relacionadas con la fuente de la [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) o [medida](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FontName>...</FontName>  
   ...  
</CalculationProperty>  
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
|Elementos primarios|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **FontName** propiedad contiene una expresión de expresiones multidimensionales (MDX) y se aplica a **CalculationProperty** elementos que tienen un [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) de *Miembro* o *celdas*.  
  
 Los elementos que corresponden a los elementos primarios de **FontName** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.CalculationProperty> y <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
