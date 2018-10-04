---
title: Nivel de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Level Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LEVEL
helpviewer_keywords:
- Level element
ms.assetid: 66ee2c16-d6b8-4dd3-879f-1f2b6923bc43
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b057f53f04003755fecf4f297012559d48c6f09d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048252"
---
# <a name="level-element-assl"></a>Elemento Level (ASSL)
  Define un nivel en un [jerarquía](hierarchy-element-assl.md) elemento.  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Levels](../collections/levels-element-assl.md)|  
|Elementos secundarios|[Las anotaciones](../collections/annotations-element-assl.md), [descripción](../properties/description-element-assl.md), [HideMemberIf](../properties/hidememberif-element-assl.md), [ID](../properties/id-element-assl.md), [nombre](../properties/name-element-assl.md), [SourceAttributeID](../properties/attributeid-element-assl.md), [Traducciones](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Este tipo de datos no tiene ninguna restricción en ningún modo de implementación (1-Multidimensional y minería de datos, 2-SharePoint y 3-Tabular).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Level>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
