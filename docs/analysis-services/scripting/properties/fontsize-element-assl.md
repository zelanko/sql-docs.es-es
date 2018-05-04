---
title: Elemento FontSize (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- FontSize Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- FontSize
helpviewer_keywords:
- FontSize element
ms.assetid: 49f66a73-946a-4fbd-9749-a3ca1b717ff3
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: baa220dddc1e6c368ad9880c6d78f14fa94b39f7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fontsize-element-assl"></a>Elemento FontSize (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe las características de presentación relacionadas con la fuente de la [CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md) o [medida](../../../analysis-services/scripting/objects/measure-element-assl.md) elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <FontSize>...</FontSize>  
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
 El **FontSize** propiedad contiene una expresión de expresiones multidimensionales (MDX) y se aplica a **CalculationProperty** elementos que tienen un [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) de *Miembro* o *celdas*.  
  
 Los elementos que corresponden a los elementos primarios de **FontSize** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.CalculationProperty> y <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
