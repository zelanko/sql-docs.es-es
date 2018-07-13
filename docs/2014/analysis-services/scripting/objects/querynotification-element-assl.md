---
title: Elemento QueryNotification (ASSL) | Microsoft Docs
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
- QueryNotification Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- QueryNotification element
ms.assetid: 0ee06730-81ff-4913-96e6-f39b6f181650
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7d31cef8ee52964bf9aeb0c7c489f2831f5cb80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153306"
---
# <a name="querynotification-element-assl"></a>Elemento QueryNotification (ASSL)
  Contiene información para el elemento [ProactiveCaching](proactivecaching-element-assl.md) sobre la consulta que se va a ejecutar para determinar si se ha modificado un origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<QueryNotifications>  
   <QueryNotification>  
      <Query>...</Query>  
...</QueryNotification>  
</QueryNotifications>  
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
|Elementos primarios|[QueryNotifications](../collections/querynotifications-element-assl.md)|  
|Elementos secundarios|[Consulta](../properties/query-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.QueryNotification>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos ProactiveCachingQueryBinding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
