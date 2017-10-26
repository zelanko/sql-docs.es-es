---
title: Elemento Latency (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Latency Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Latency
helpviewer_keywords:
- Latency element
ms.assetid: 93940637-b83e-4773-b80d-3394ca3a1ce5
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c4e6dec17b87a714f15c022f3ba4f51fa26c95a7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="latency-element-assl"></a>Elemento Latency (ASSL)
  Define el "período de gracia" entre la notificación más antigua y el momento en el que se destruyen las imágenes OLAP multidimensionales (MOLAP).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ProactiveCaching>  
   ...  
   <Latency>...</Latency>  
   ...  
</ProactiveCaching element>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|duración|  
|Valor predeterminado|P0s|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que corresponde al elemento primario de **latencia** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

