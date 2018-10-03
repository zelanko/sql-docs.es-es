---
title: Elemento IncrementalProcessingNotification (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- IncrementalProcessingNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- IncrementalProcessingNotification element
ms.assetid: bfc9b0a4-4043-4aaf-82d9-67e7f1d1eb81
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 639d58928b27e965a707602c0ea124c9078e5b47
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120745"
---
# <a name="incrementalprocessingnotification-element-assl"></a>Elemento IncrementalProcessingNotification (ASSL)
  Contiene información para el [ProactiveCaching](proactivecaching-element-assl.md) elemento sobre una consulta que se ejecutan para determinar el progreso del procesamiento incremental.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<IncrementalProcessingNotifications>  
   <IncrementalProcessingNotification xsi:type="IncrementalProcessingNotification">...</IncrementalProcessingNotification>  
</IncrementalProcessingNotifications>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[IncrementalProcessingNotification](../data-type/incrementalprocessingnotification-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[IncrementalProcessingNotifications](../collections/incrementalprocessingnotifications-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ProactiveCachingQueryBinding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Elemento ProactiveCaching &#40;ASSL&#41;](proactivecaching-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
