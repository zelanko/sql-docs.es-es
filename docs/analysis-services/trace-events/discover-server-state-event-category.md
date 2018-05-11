---
title: Detectar la categoría de eventos de estado del servidor | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 83bad9f141c0da4918f7558f0b34b7816e51d737
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="discover-server-state-event-category"></a>detección de estado del servidor, categoría de eventos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La categoría de eventos Detección de estado del servidor tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|Recopila todos los eventos de inicio de detección XMLA de estado de servidor desde que se inició el seguimiento.|  
|Server State Discover Data|34|Recopila todos los eventos de detección XMLA de estado de servidor desde que se inició el seguimiento. Estos eventos capturan el contenido de la respuesta a la solicitud de detección.|  
|Server State Discover End|35|Recopila todos los eventos de fin de detección XMLA de estado de servidor desde que se inició el seguimiento.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de evento de Eventos de consultas, vea [Discover Server State Events Data Columns](../../analysis-services/trace-events/discover-server-state-events-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
