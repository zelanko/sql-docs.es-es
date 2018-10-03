---
title: Elemento Events (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Events Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Events
helpviewer_keywords:
- Events element
ms.assetid: de887998-dc4b-44dc-8fec-08d67b92f96d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f336d2a265a6a427d2b2674ac233c0468fb63e8f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197787"
---
# <a name="events-element-assl"></a>Elemento Events (ASSL)
  Define la colección de los elementos [Event](../objects/event-element-assl.md) que va a capturar un [Trace](../objects/trace-element-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Trace>  
   ...  
   <Events>  
      <Event>...</Event>  
   </Events>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Seguimiento](../objects/trace-element-assl.md)|  
|Elementos secundarios|[Evento](../objects/event-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TraceEventCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Realiza un seguimiento de elemento &#40;ASSL&#41;](traces-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
