---
title: Elemento Trace (ASSL) | Documentos de Microsoft
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
- Trace Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Trace
helpviewer_keywords:
- Trace element
ms.assetid: dda9136a-a9c1-44a1-b8d3-b0ec4dc65c87
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bb089bc193316a56ab0a7355411178ece44c8788
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103170"
---
# <a name="trace-element-assl"></a>Elemento Trace (ASSL)
  Define un seguimiento que se puede consultar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      Profiler syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LogFileName>...</LogFileName>  
      <LogFileAppend>...</LogFileAppend>  
      <LogFileSize>...</LogFileSize>  
      <Audit>...</Audit>  
      <LogFileRollover>...</LogFileRollover>  
      <AutoRestart>...</AutoRestart>  
      <StopTime>...</StopTime>  
      <Filter>...</Filter>  
      <Events>...</Events>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
```  
  
      Extended Events syntax  
<Traces>  
   <Trace>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <XEvent>...</XEvent>  
      <Annotations>...</Annotations>  
   </Trace>  
</Traces>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Seguimientos](../collections/traces-element-assl.md)|  
|Elementos secundarios|[Annotations](../collections/annotations-element-assl.md), [Audit](../properties/audit-element-assl.md), [AutoRestart](../properties/autorestart-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [Description](../properties/description-element-assl.md), [Events](../collections/events-element-assl.md), [Filter](../properties/filter-element-trace-assl.md), [ID](../properties/id-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [LogFileAppend](../properties/logfileappend-element-assl.md), [LogFileName](../properties/name-element-assl.md), [LogFileRollover](../properties/logfilerollover-element-assl.md), [LogFileSize](../properties/logfilesize-element-assl.md), [Name](../properties/name-element-assl.md), [StopTime](../properties/stoptime-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Server &#40;ASSL&#41;](server-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  