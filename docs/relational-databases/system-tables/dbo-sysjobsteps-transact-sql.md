---
title: dbo.sysjobsteps (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysjobsteps
- dbo.sysjobsteps_TSQL
- sysjobsteps
- sysjobsteps_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobsteps system table
ms.assetid: 978b8205-535b-461c-91f3-af9b08eca467
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5fff8cb852214733a96d1641cd767d578420cb9a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysjobsteps-transact-sql"></a>dbo.sysjobsteps (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene la información de cada paso de un trabajo que debe ejecutar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Id. del trabajo.|  
|**step_id**|**int**|Id. del paso en el trabajo.|  
|**Step_name**|**sysname**|Nombre del paso del trabajo.|  
|**subsystem**|**nvarchar(40)**|Nombre del subsistema que utiliza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar el paso del trabajo.|  
|**command**|**nvarchar(max)**|Comando que ejecutará **subsistema**.|  
|**flags**|**int**|Reservado.|  
|**additional_parameters**|**ntext**|Reservado.|  
|**cmdexec_success_code**|**int**|Valor de nivel de error devuelto por **CmdExec** pasos del subsistema para indicar una operación correcta.|  
|**on_success_action**|**tinyint**|Acción que se debe realizar cuando un paso se ejecuta correctamente.|  
|**on_success_step_id**|**int**|Id. del siguiente paso que se debe ejecutar cuando un paso se ejecuta correctamente.|  
|**on_fail_action**|**tinyint**|Acción que se debe realizar cuando un paso no se ejecuta correctamente.|  
|**on_fail_step_id**|**int**|Id. del siguiente paso que se debe ejecutar cuando un paso no se ejecuta correctamente.|  
|**servidor**|**sysname**|Reservado.|  
|**database_name**|**sysname**|Nombre de la base de datos en el que **comando** se ejecuta si **subsistema** es TSQL.|  
|**database_user_name**|**sysname**|Nombre del usuario de base de datos cuya cuenta se utiliza al ejecutar el paso.|  
|**retry_attempts**|**int**|Número de reintentos si el paso no se ejecuta correctamente.|  
|**retry_interval**|**int**|Tiempo que se debe esperar entre cada intento.|  
|**os_run_priority**|**int**|Reservado.|  
|**output_file_name**|**nvarchar(200)**|Nombre del archivo en el que la salida del paso se guarda cuando **subsistema** es TSQL, PowerShell o **CmdExec ***.*|  
|**last_run_outcome**|**int**|Resultado de la ejecución anterior del paso del trabajo.<br /><br /> **0** = error<br /><br /> **1** = se ha realizado correctamente<br /><br /> **2** = reintento<br /><br /> **3** = cancelado<br /><br /> **5** = desconocido|  
|**last_run_duration**|**int**|Duración (hhmmss) del paso la última vez que se ejecutó.|  
|**last_run_retries**|**int**|Número de reintentos en la última ejecución del paso del trabajo.|  
|**last_run_date**|**int**|Fecha (aaaammdd) en que se inició la ejecución del paso por última vez.|  
|**last_run_time**|**int**|Hora (hhmmss) en que se inició la ejecución del paso por última vez.|  
|**proxy_id**|**int**|Proxy del paso de trabajo.|  
|**step_uid**|**uniqueidentifier**|Identificador del paso de trabajo.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sql-server-agent-tables-transact-sql.md)  
  
  
