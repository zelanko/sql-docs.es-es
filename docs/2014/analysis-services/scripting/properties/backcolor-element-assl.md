---
title: Elemento BackColor (ASSL) | Microsoft Docs
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
- BackColor Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- BackColor
helpviewer_keywords:
- BackColor element
ms.assetid: 9024d131-74cc-4815-833a-f8cae57b7453
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ed491d6307e6e5776843c3f5e490d9369235143b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274121"
---
# <a name="backcolor-element-assl"></a>Elemento BackColor (ASSL)
  Describe las características de presentación del elemento principal relacionadas con el color.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty> <!-- or Measure -->  
   ...  
   <BackColor>...</BackColor>  
   ...  
</CalculationProperty>  
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
|Elemento primario|[CalculationProperty](../objects/calculationproperty-element-assl.md), [medida](../objects/measure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `BackColor` propiedad contiene una expresión de lenguaje de expresiones multidimensionales (MDX) y se aplica a `CalculationProperty` elementos con un [CalculationType](calculationtype-element-assl.md) de *miembro* o  *Las celdas*.  
  
 El elemento que se corresponde con el elemento primario de `BackColor` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
