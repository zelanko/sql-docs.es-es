---
title: Alerts (objeto del Agente SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: befda35956a04617cf9307aa7cb2fd41e8f7cd03
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198669"
---
# <a name="sql-server-agent-alerts-object"></a>Alerts (objeto del Agente SQL Server)
  El objeto de rendimiento **Alerts** del Agente SQL Server contiene contadores de rendimiento que proporcionan información acerca del Agente SQL Server. En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
 La tabla siguiente contiene los contadores **SQLAgent:Alerts** .  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Alertas activadas**|Este contador indica el número total de alertas que el Agente SQL Server ha activado desde la última vez que se reinició.|  
|**Alertas activadas/minuto**|Este contador indica el número de alertas que activó el Agente SQL Server en el último minuto.|  
  
> [!NOTE]  
>  Para usar este objeto del Agente SQL Server, los usuarios deben ser miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="see-also"></a>Vea también  
 [Alerts](../../ssms/agent/alerts.md)   
 [Usar objetos de rendimiento](../../ssms/agent/use-performance-objects.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  