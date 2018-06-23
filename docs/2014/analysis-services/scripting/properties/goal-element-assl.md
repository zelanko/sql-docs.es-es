---
title: Elemento goal (ASSL) | Documentos de Microsoft
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
- Goal Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Goal
helpviewer_keywords:
- Goal element
ms.assetid: 75fa5b57-418e-43ad-8704-764e4f0a40cf
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8b408e73bd8cb376afe0b8cf36157628be908780
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103924"
---
# <a name="goal-element-assl"></a>Elemento Goal (ASSL)
  Identifica el objetivo deseado en un [Kpi](../objects/kpi-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Kpi>  
   ...  
   <Goal>...</Goal>  
   ...  
</Kpi>  
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
|Elemento primario|[KPI](../objects/kpi-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `Goal` contiene una expresión MDX (Expresiones multidimensionales).  
  
 El elemento que corresponde al elemento primario de `Goal` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Kpi>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Status &#40;ASSL&#41;](status-element-assl.md)   
 [Elemento de tendencia &#40;ASSL&#41;](trend-element-assl.md)   
 [Valor de elemento &#40;ASSL&#41;](value-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  