---
title: dbo.sysjobactivity (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobactivity_TSQL
- dbo.sysjobactivity
- sysjobactivity
- sysjobactivity_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobactivity system table
ms.assetid: fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0b7991dfbe4aee731d436d725aba2081adf87e84
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobactivity-transact-sql"></a>dbo.sysjobactivity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra la actividad y el estado de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual.  Esta tabla se almacena en la **msdb** base de datos.
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Identificador de la sesión almacenada en el **syssessions** tabla el **msdb** base de datos.|  
|**job_id**|**uniqueidentifier**|Id. del trabajo.|  
|**run_requested_date**|**datetime**|Fecha y hora en que se solicitó la ejecución del trabajo.|  
|**run_requested_source**|**sysname(nvarchar(128))**|Solicitante de la ejecución del trabajo.<br /><br /> **1** = SOURCE_SCHEDULER<br /><br /> **2** = SOURCE_ALERTER<br /><br /> **3** = SOURCE_BOOT<br /><br /> **4** = SOURCE_USER<br /><br /> **6** = SOURCE_ON_IDLE_SCHEDULE|  
|**queued_date**|**datetime**|Fecha y hora en que el trabajo se puso en cola. Si el trabajo se ejecuta directamente, esta columna es NULL.|  
|**start_execution_date**|**datetime**|Fecha y hora de la programación de la ejecución del trabajo.|  
|**last_executed_step_id**|**int**|Id. del último paso de trabajo que se ejecutó.|  
|**last_executed_step_**<br /><br /> **date**|**datetime**|Fecha y hora en que empezó a ejecutarse el último paso de trabajo.|  
|**stop_execution_date**|**datetime**|Fecha y hora de finalización de la ejecución del trabajo.|  
|**job_history_id**|**int**|Usado para identificar una fila en la **sysjobhistory** tabla.|  
|**next_scheduled_run_date**|**datetime**|Siguiente fecha y hora en que se ha programado la ejecución del trabajo.|  

## <a name="example"></a>Ejemplo
Este ejemplo devuelve el estado de tiempo de ejecución para todos los trabajos del Agente SQL Server.  Ejecute la siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
```tsql
SELECT sj.Name, 
    CASE
        WHEN sja.start_execution_date IS NULL THEN 'Not running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NULL THEN 'Running'
        WHEN sja.start_execution_date IS NOT NULL AND sja.stop_execution_date IS NOT NULL THEN 'Not running'
    END AS 'RunStatus'
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobactivity sja
ON sj.job_id = sja.job_id
WHERE session_id = (
    SELECT MAX(session_id) FROM msdb.dbo.sysjobactivity); 
```
  
## <a name="see-also"></a>Vea también  
 [dbo.sysjobhistory &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
  
  
