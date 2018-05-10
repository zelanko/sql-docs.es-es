---
title: Categoría de eventos de bloqueo | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 46148326b3351340a57a26d445a225cbbea35220
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="lock-events-category"></a>Bloqueo (categoría de eventos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
