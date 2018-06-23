---
title: Un nivel de elemento (ASSL) | Documentos de Microsoft
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
- Levels Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Levels
helpviewer_keywords:
- Levels element
ms.assetid: a9dd4890-a5da-48e7-9bbf-f857107cde8d
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: aafc68525f656f77eca7c8cdcd0fdc4cb4534791
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112336"
---
# <a name="levels-element-assl"></a>Elemento Levels (ASSL)
  Contiene la colección de [nivel](../objects/level-element-assl.md) elementos en una [jerarquía](../objects/hierarchy-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Hierarchy>  
      ...  
   <Levels>  
      <Level>...</Level>  
   </Levels>  
   ...  
</Hierarchy>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Hierarchy](../objects/hierarchy-element-assl.md)|  
|Elementos secundarios|[Level](../objects/level-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.LevelCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  