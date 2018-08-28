---
title: Alerts (objeto del Agente SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d310d463d0cb20135b1318f6ffd27c0b602f33e4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406642"
---
# <a name="sql-server-agent-alerts-object"></a>Alerts (objeto del Agente SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto de rendimiento **Alerts** del Agente SQL Server contiene contadores de rendimiento que proporcionan información acerca del Agente SQL Server. En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
 La tabla siguiente contiene los contadores **SQLAgent:Alerts** .  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Alertas activadas**|Este contador indica el número total de alertas que el Agente SQL Server ha activado desde la última vez que se reinició.|  
|**Alertas activadas/minuto**|Este contador indica el número de alertas que activó el Agente SQL Server en el último minuto.|  
  
> [!NOTE]  
>  Para usar este objeto del Agente SQL Server, los usuarios deben ser miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="see-also"></a>Ver también  
 [Alerts](../../ssms/agent/alerts.md)   
 [Usar objetos de rendimiento](../../ssms/agent/use-performance-objects.md)   
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
