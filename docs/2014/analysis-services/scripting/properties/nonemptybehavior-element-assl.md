---
title: Elemento NonEmptyBehavior (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- NonEmptyBehavior Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NonEmptyBehavior
helpviewer_keywords:
- NonEmptyBehavior element
ms.assetid: b4c78af4-b049-4189-a35b-206e3938d1db
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eda18e3ed67884e964439e80e0ae0103f522e116
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183302"
---
# <a name="nonemptybehavior-element-assl"></a>Elemento NonEmptyBehavior (ASSL)
  Determina el comportamiento de no vacío asociado al elemento primario de la [CalculationProperty](../objects/calculationproperty-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty>  
  
   <NonEmptyBehavior>...</NonEmptyBehavior>  
  
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
|Elemento primario|[CalculationProperty](../objects/calculationproperty-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `NonEmptyBehavior` propiedad se aplica a `CalculationProperty` elementos con un [CalculationType](calculationtype-element-assl.md) establecido en *miembro*.  
  
 El elemento que se corresponde con el elemento primario de `NonEmptyBehavior` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.CalculationProperty>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
