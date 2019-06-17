---
title: Alerts (objeto del Agente SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: ca1234a9b70c3da26ed9146e4c5eda51ca431f80
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62671654"
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
  
## <a name="see-also"></a>Consulte también  
 [Alerts](../../ssms/agent/alerts.md)   
 [Usar objetos de rendimiento](../../ssms/agent/use-performance-objects.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
