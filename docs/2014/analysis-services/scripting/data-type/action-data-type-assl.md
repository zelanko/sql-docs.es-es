---
title: Tipo de datos Action (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Action Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Action data type
ms.assetid: 8c4d2ff7-17e1-4e74-bec7-637e0b191acf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21c13562fa53c0ba396a4c3826889e8d275f7d9a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197495"
---
# <a name="action-data-type-assl"></a>Tipo de datos Action (ASSL)
  Define un tipo de datos primitivo abstracto que representa una acción en un [cubo](../objects/cube-element-assl.md) elemento o un [perspectiva](../objects/perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Action>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Caption>...</Caption>  
      <CaptionIsMdx>...</CaptionIsMdx>  
      <Translations>...</Translations>  
   <TargetType>...</TargetType>  
   <Target>...</Target>  
   <Condition>...</Condition>  
   <Type>...</Type>  
   <Invocation>...</Invocation>  
   <Application>...</Application>  
      <Description>...</Description>  
      <Annotations>...</Annotations>  
</Action>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acciones](../collections/actions-element-assl.md)|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [aplicación](../properties/application-element-assl.md), [título](../properties/caption-element-assl.md), [CaptionIsMdx](../properties/captionismdx-element-assl.md), [condición](../properties/condition-element-assl.md), [descripción ](../properties/description-element-assl.md), [ID](../properties/id-element-assl.md), [invocación](../properties/invocation-element-assl.md), [nombre](../properties/name-element-assl.md), [destino](../properties/target-element-assl.md), [TargetType](../properties/targettype-element-assl.md), [Traducciones](../collections/translations-element-assl.md), [tipo](../properties/type-element-action-assl.md)|  
|Elementos derivados|[DrillThroughAction](action-data-type-assl.md), [ReportAction](reportaction-data-type-assl.md), [StandardAction](standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para más información sobre las acciones, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](../../multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](../objects/cube-element-assl.md)   
 [Elemento Perspective &#40;ASSL&#41;](../objects/perspective-element-assl.md)   
 [Tipo de datos PerspectiveAction &#40;ASSL&#41;](perspectiveaction-data-type-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
