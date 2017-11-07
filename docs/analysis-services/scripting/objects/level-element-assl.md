---
title: Nivel de elemento (ASSL) | Documentos de Microsoft
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
- Level Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- LEVEL
helpviewer_keywords:
- Level element
ms.assetid: 66ee2c16-d6b8-4dd3-879f-1f2b6923bc43
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c25abef64207476f0b0401ace9d120a35fd56730
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="level-element-assl"></a>Elemento Level (ASSL)
  Define un nivel en un [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Levels>  
      <Level>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <SourceAttributeID>...</SourceAttributeID>  
      <HideMemberIf>...</HideMemberIf>  
      <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Level>  
</Levels>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Levels](../../../analysis-services/scripting/collections/levels-element-assl.md)|  
|Elementos secundarios|[Anotaciones](../../../analysis-services/scripting/collections/annotations-element-assl.md), [descripción](../../../analysis-services/scripting/properties/description-element-assl.md), [HideMemberIf](../../../analysis-services/scripting/properties/hidememberif-element-assl.md), [identificador](../../../analysis-services/scripting/properties/id-element-assl.md), [nombre](../../../analysis-services/scripting/properties/name-element-assl.md), [SourceAttributeID](../../../analysis-services/scripting/properties/sourceattributeid-element-assl.md), [Traducciones](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este tipo de datos no tiene ninguna restricción en ningún modo de implementación (1-Multidimensional y minería de datos, 2-SharePoint y 3-Tabular).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Level>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos de &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

