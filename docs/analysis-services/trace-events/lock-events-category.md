---
title: Categoría de eventos de bloqueo | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 7e1b7a18c7ed5f763674ade69647a26f775cfb98
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
  
