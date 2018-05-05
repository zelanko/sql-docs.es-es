---
title: Detectar la categoría de eventos de estado del servidor | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Discover Server State event category
- server state events [Analysis Services]
- discover server state events
- event classes [Analysis Services], discover server state
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: be6fb98d3f4a7dcb710e81ff5e0410ac43ec958f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
  
