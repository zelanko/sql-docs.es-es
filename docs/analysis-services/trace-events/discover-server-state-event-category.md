---
title: "Detecci&#243;n de estado del servidor (categor&#237;a de eventos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "detección de estado del servidor, categoría de eventos"
  - "estado del servidor, eventos [Analysis Services]"
  - "detección de estado del servidor, eventos"
  - "clases de eventos [Analysis Services], detectar el estado del servidor"
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 25
---
# Detecci&#243;n de estado del servidor (categor&#237;a de eventos)
  La categoría de eventos Detección de estado del servidor tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|Recopila todos los eventos de inicio de detección XMLA de estado de servidor desde que se inició el seguimiento.|  
|Server State Discover Data|34|Recopila todos los eventos de detección XMLA de estado de servidor desde que se inició el seguimiento. Estos eventos capturan el contenido de la respuesta a la solicitud de detección.|  
|Server State Discover End|35|Recopila todos los eventos de fin de detección XMLA de estado de servidor desde que se inició el seguimiento.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de evento de Eventos de consultas, vea [Discover Server State Events Data Columns](../../analysis-services/trace-events/discover-server-state-events-data-columns.md).  
  
## Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  