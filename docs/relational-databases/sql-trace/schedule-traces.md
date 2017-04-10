---
title: "Programar seguimientos | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "filtros [SQL Server], eventos"
  - "seguimientos [SQL Server]"
  - "seguimientos [SQL Server], detener"
  - "eventos [SQL Server], filtros"
  - "programar seguimientos [SQL Server]"
  - "seguimientos [SQL Server], programar"
  - "detener seguimientos"
ms.assetid: 620b79db-924b-4502-8af3-39efcfca245d
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# Programar seguimientos
  En Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hay dos formas de programar trazas. Puede hacer lo siguiente:  
  
-   Habilitar una hora de detención de seguimiento.  
  
-   Utilizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar una seguimiento.  
  
## Especificar una hora de detención  
 Puede especificar una hora de detención de seguimiento si utiliza procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] o si utiliza el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. La hora de detención debe establecerse al configurar originalmente la seguimiento.  
  
## Programar seguimientos mediante el Agente SQL Server  
 La mejor forma de programar seguimientos consiste en usar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar el seguimiento y, después, especificar una hora de detención de seguimiento mediante el procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_trace_setstatus** o el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 **Para establecer un filtro de hora de finalización para una seguimiento**  
  
 [Filtrar eventos basándose en la hora de finalización del evento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-based-on-the-event-end-time-sql-server-profiler.md)  
  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
## Vea también  
 [Tareas administrativas automatizadas &#40;Agente SQL Server&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)  
  
  