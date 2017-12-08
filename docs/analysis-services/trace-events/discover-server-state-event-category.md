---
title: "Detectar la categoría de eventos de estado del servidor | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Discover Server State event category
- server state events [Analysis Services]
- discover server state events
- event classes [Analysis Services], discover server state
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f553fc692cb15d5393718c3b40d2c5d33dbcf222
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="discover-server-state-event-category"></a>detección de estado del servidor, categoría de eventos
  La categoría de eventos Detección de estado del servidor tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|Recopila todos los eventos de inicio de detección XMLA de estado de servidor desde que se inició el seguimiento.|  
|Server State Discover Data|34|Recopila todos los eventos de detección XMLA de estado de servidor desde que se inició el seguimiento. Estos eventos capturan el contenido de la respuesta a la solicitud de detección.|  
|Server State Discover End|35|Recopila todos los eventos de fin de detección XMLA de estado de servidor desde que se inició el seguimiento.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de evento de Eventos de consultas, vea [Discover Server State Events Data Columns](../../analysis-services/trace-events/discover-server-state-events-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
