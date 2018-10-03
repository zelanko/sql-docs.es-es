---
title: Elemento FontName (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- FontName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- FontName
helpviewer_keywords:
- FontName element
ms.assetid: 5560a852-9745-4abb-93d8-9cebe8a9897c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f3894711625d1ea121e7744a0d58ed46ac6cafa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090545"
---
# <a name="fontname-element-assl"></a>Elemento FontName (ASSL)
  Describe las características de presentación relacionadas con la fuente de la [CalculationProperty](../objects/calculationproperty-element-assl.md) o [medida](../objects/measure-element-assl.md) elemento primario.  
  
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
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CalculationProperty](../objects/calculationproperty-element-assl.md), [medida](../objects/measure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El `FontName` propiedad contiene una expresión MDX (expresiones multidimensionales) y se aplica a `CalculationProperty` los elementos que tienen un [CalculationType](calculationtype-element-assl.md) de *miembro* o *celdas* .  
  
 Los elementos que corresponden a los elementos primarios de `FontName` en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.CalculationProperty> y <xref:Microsoft.AnalysisServices.Measure>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
