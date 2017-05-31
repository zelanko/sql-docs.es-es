---
title: Jobs (objeto del Agente SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a8f2931c070c0ed3816fb348b4ca41f3705b19a0
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-agent-jobs-object"></a>Jobs (objeto del Agente SQL Server)
  El objeto de rendimiento **Jobs** del Agente SQL Server contiene contadores de rendimiento que proporcionan información acerca de los trabajos del Agente SQL Server. En la siguiente tabla se enumeran los contadores incluidos en este objeto.  
  
 La tabla siguiente contiene los contadores de **SQLAgent:Jobs** .  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Trabajos activos**|Este contador muestra el número de trabajos que se están ejecutando.|  
|**Trabajos con error**|Este contador muestra el número de trabajos que han terminado con un error.|  
|**Tasa de trabajos con éxito**|Este contador muestra el porcentaje de trabajos ejecutados que se han completado con éxito.|  
|**Trabajos activados/minuto**|Este contador muestra el número de trabajos que se han iniciado en el último minuto.|  
|**Trabajos en cola**|Este contador muestra el número de trabajos preparados para que el Agente SQL Server pueda ejecutarlos, pero que aún no se están ejecutando.|  
|**Trabajos con éxito**|Este contador muestra el número de trabajos que han terminado con éxito.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Instancia|Descripción|  
|--------------|-----------------|  
|**_Total**|Información para todos los trabajos.|  
|**Alertas**|Información de los trabajos iniciados por las alertas.|  
|**Otros**|Información de los trabajos no iniciados por alertas ni programaciones. Normalmente estos trabajos de inician de forma manual mediante **sp_start_job**.|  
|**Programaciones**|Información de los trabajos iniciados por las programaciones.|  
  
## <a name="see-also"></a>Vea también  
 [Implementar trabajos](http://msdn.microsoft.com/library/69e06724-25c7-4fb3-8a5b-3d4596f21756)   
 [Usar objetos de rendimiento](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
