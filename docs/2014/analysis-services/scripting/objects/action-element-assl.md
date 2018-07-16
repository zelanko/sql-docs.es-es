---
title: Elemento Action (ASSL) | Microsoft Docs
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
- Action Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Action
helpviewer_keywords:
- Action element
ms.assetid: aaee06a2-91c6-4007-b787-79cb08d63c77
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bfc51d797852e80cf7bf501cf3f1d93f2f52c9d9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196015"
---
# <a name="action-element-assl"></a>Elemento Action (ASSL)
  Contiene información sobre una acción disponible en un [cubo](cube-element-assl.md) elemento o un [perspectiva](perspective-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Actions>  
   <Action xsi:type="DrillThroughAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="ReportAction">...</Action> <!-- ancestor: Cube -->  
   <Action xsi:type="StandardAction">...</Action> <!-- ancestor: Cube -->  
   <!-- or -->  
   <Action xsi:type="PerspectiveAction">...</Action> <!-- ancestor: Perspective -->  
</Actions>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
|Antecesor o elemento primario|Tipo de datos|  
|------------------------|---------------|  
|[Cubo](../data-type/action-data-type-assl.md), [ReportAction](../data-type/reportaction-data-type-assl.md), [StandardAction](../data-type/standardaction-data-type-assl.md)|  
|[Perspectiva](../data-type/perspectiveaction-data-type-assl.md)|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Acciones](../collections/actions-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Action>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de cubo &#40;ASSL&#41;](cube-element-assl.md)   
 [Elemento Perspective &#40;ASSL&#41;](perspective-element-assl.md)   
 [Tipo de datos PerspectiveAction &#40;ASSL&#41;](../data-type/perspectiveaction-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
