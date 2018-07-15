---
title: Elemento Event (ASSL) | Microsoft Docs
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
- Event Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EVENT
helpviewer_keywords:
- Event element
ms.assetid: c7911bcd-e601-4a96-a6d8-20b7c7375ff2
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 119bc279e1313e0b7b8bd0790c631b8e9a896428
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233885"
---
# <a name="event-element-assl"></a>Elemento Event (ASSL)
  Define un `Event` debe capturar como parte de un [seguimiento](trace-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Events>  
   <Event>  
      <EventID>...</EventID>  
      <Columns>...</Columns>  
   </Event>  
</Events>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Eventos](../collections/events-element-assl.md)|  
|Elementos secundarios|[Columnas](../collections/columns-element-assl.md), [EventID](../properties/id-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TraceEvent>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Trace &#40;ASSL&#41;](trace-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
