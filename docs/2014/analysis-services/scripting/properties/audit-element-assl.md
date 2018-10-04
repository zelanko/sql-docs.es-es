---
title: Elemento (ASSL) de auditoría | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Audit Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Audit
helpviewer_keywords:
- Audit element
ms.assetid: 26488119-6490-426d-a4e4-274b5bdffbc2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 283be4682a7dd5742b93cba596efc87322a1d539
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097439"
---
# <a name="audit-element-assl"></a>Elemento Audit (ASSL)
  Especifica que un [seguimiento](../objects/trace-element-assl.md) elemento no puede quitar cualquier evento, aún cuando esto produce una reducción del rendimiento en el servidor.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Trace>  
   ...  
   <Audit>...</Audit>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|`False`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Seguimiento](../objects/trace-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `Audit` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Vea también  
 [Realiza un seguimiento de elemento &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
