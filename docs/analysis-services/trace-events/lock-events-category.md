---
title: "Categoría de eventos de bloqueo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4fbe7cccb4caaa0b87a7f502ed3ca714e3efa515
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lock-events-category"></a>Bloqueo (categoría de eventos)
  La categoría de eventos de bloqueo tiene las clases de eventos que se describen en la siguiente tabla.  
  
|Clase de eventos|Identificador del evento|Description|  
|-----------------|--------------|-----------------|  
|Deadlock|50|Recopila todos los eventos de interbloqueo de bloqueos de metadatos desde que se inició el seguimiento.|  
|Lock timeout|51|Recopila todos los eventos de tiempo de espera de bloqueos de metadatos desde que se inició el seguimiento.|  
|Lock Acquired|52|Recopila información sobre los bloqueos adquiridos desde que comenzó el seguimiento.|  
|Lock Released|53|Recopila información sobre los bloqueos liberados desde que comenzó el seguimiento.|  
|Lock Waiting|54|Recopila información sobre los bloqueos en estado de espera desde que comenzó el seguimiento.|  
  
 Para obtener más información acerca de las columnas asociadas a cada una de las clases de eventos de bloqueo, vea [Lock Events Data Columns](../../analysis-services/trace-events/lock-events-data-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  

