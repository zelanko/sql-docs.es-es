---
title: Tipo de datos Action (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b717929c61852836527f00809528ccb8d2b26d8d
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34037276"
---
# <a name="action-data-type-assl"></a>Tipo de datos Action (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos primitivo abstracto que representa una acción en el elemento [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md) o en el elemento [Perspective](../../../analysis-services/scripting/objects/perspective-element-assl.md) .  
  
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
|Tipos de datos base|Ninguno|  
|Tipos de datos derivados|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acciones](../../../analysis-services/scripting/collections/actions-element-assl.md)|  
|Elementos secundarios|[Anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [aplicación](../../../analysis-services/scripting/properties/application-element-assl.md), [título](../../../analysis-services/scripting/properties/caption-element-assl.md), [CaptionIsMdx](../../../analysis-services/scripting/properties/captionismdx-element-assl.md), [condición](../../../analysis-services/scripting/properties/condition-element-assl.md), [descripción ](../../../analysis-services/scripting/properties/description-element-assl.md), [Identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [invocación](../../../analysis-services/scripting/properties/invocation-element-assl.md), [nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [destino](../../../analysis-services/scripting/properties/target-element-assl.md), [TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md), [Traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md), [tipo](../../../analysis-services/scripting/properties/type-element-action-assl.md)|  
|Elementos derivados|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md), [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md), [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para más información sobre las acciones, vea [Acciones &#40;Analysis Services - Datos multidimensionales&#41;](../../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [CUBE, elemento & #40; ASSL & #41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Perspective, elemento & #40; ASSL & #41;](../../../analysis-services/scripting/objects/perspective-element-assl.md)   
 [Tipo de datos PerspectiveAction & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)   
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
