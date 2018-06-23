---
title: Elemento Events (ASSL) | Documentos de Microsoft
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
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a9fd96d0ad375725d1b7efa72dda9c0467e0b93b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114338"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
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
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TraceEventCollection>.  
  
## <a name="see-also"></a>Vea también  
 [Realiza un seguimiento de elemento &#40;ASSL&#41;](traces-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  