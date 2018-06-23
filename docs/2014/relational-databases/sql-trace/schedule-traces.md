---
title: Programar seguimientos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- traces [SQL Server]
- traces [SQL Server], stopping
- events [SQL Server], filters
- scheduling traces [SQL Server]
- traces [SQL Server], scheduling
- stopping traces
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3017f239b024bcab3d19b589be1ec189187a5d09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108053"
---
# <a name="schedule-traces"></a>Programar seguimientos
  En Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hay dos formas de programar trazas. Puede hacer lo siguiente:  
  
-   Habilitar una hora de detención de seguimiento.  
  
-   Utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar una seguimiento.  
  
## <a name="specifying-a-stop-time"></a>Especificar una hora de detención  
 Puede especificar una hora de detención de seguimiento si utiliza procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] o si utiliza el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. La hora de detención debe establecerse al configurar originalmente la seguimiento.  
  
## <a name="scheduling-traces-by-using-sql-server-agent"></a>Programar seguimientos mediante el Agente SQL Server  
 La mejor forma de programar seguimientos consiste en usar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar el seguimiento y, después, especificar una hora de detención de seguimiento mediante el procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_trace_setstatus**o el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 **Para establecer un filtro de hora de finalización para una seguimiento**  
  
 [Filtrar eventos basándose en la hora de finalización del evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
## <a name="see-also"></a>Vea también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](../../ssms/agent/sql-server-agent.md)  
  
  
