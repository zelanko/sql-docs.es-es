---
title: dbo.sysjobhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/24/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobhistory_TSQL
- dbo.sysjobhistory
- sysjobhistory
- sysjobhistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobhistory system table
ms.assetid: 1b1fcdbb-2af2-45e6-bf3f-e8279432ce13
author: stevestein
ms.author: sstein
ms.openlocfilehash: 85710deec2e7ab5e79ed7a514e3b625c6232484e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902200"
---
# <a name="dbosysjobhistory-transact-sql"></a>dbo.sysjobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Contiene información acerca de la ejecución de los trabajos programados por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
> [!NOTE]
> En la mayoría de los casos, los datos se actualizan solo después de que se complete el paso de trabajo y la tabla normalmente no contiene ningún registro de pasos de trabajo que están actualmente en curso, pero en algunos casos de procesos subyacentes *hacer* proporcionan información acerca de pasos de trabajo de progreso.

Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Identificador único de la fila.|  
|**job_id**|**uniqueidentifier**|Id. del trabajo.|  
|**step_id**|**int**|Id. del paso en el trabajo.|  
|**step_name**|**sysname**|Nombre del paso.|  
|**sql_message_id**|**int**|Id. de los mensajes de error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devueltos si el trabajo genera algún error.|  
|**sql_severity**|**int**|Gravedad de cualquier error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**message**|**nvarchar(4000)**|Texto de un error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si existe.|  
|**run_status**|**int**|Estado de la ejecución del trabajo:<br /><br /> **0** = error<br /><br /> **1** = se ha realizado correctamente<br /><br /> **2** = reintento<br /><br /> **3** = cancelado<br /><br />**4** = en curso|  
|**run_date**|**int**|Fecha en que se empezó a ejecutar el trabajo o paso. En el caso de un historial En curso, es la fecha y hora en que fue escrito.|  
|**run_time**|**int**|Hora a la que comenzó el trabajo o paso.|  
|**run_duration**|**int**|Tiempo transcurrido en la ejecución del trabajo o paso en **HHMMSS** formato.|  
|**operator_id_emailed**|**int**|Id. del operador al que se notificó la terminación del trabajo.|  
|**operator_id_netsent**|**int**|Id. del operador al que se notificó con un mensaje la terminación del trabajo.|  
|**operator_id_paged**|**int**|Id. del operador al que se notificó por buscapersonas la terminación del trabajo.|  
|**retries_attempted**|**int**|Número de intentos de ejecución del trabajo o paso.|  
|**servidor**|**sysname**|Nombre del servidor en el que se ejecutó el trabajo.|  
  
  ## <a name="example"></a>Ejemplo
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta convertirá la **tiempo de ejecución** y **run_duration** columnas en un formato descriptivo más.  Ejecute el script en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 
 ```sql
 SET NOCOUNT ON;
 
 SELECT sj.name,
        sh.run_date,
        sh.step_name,
        STUFF(STUFF(RIGHT(REPLICATE('0', 6) +  CAST(sh.run_time as varchar(6)), 6), 3, 0, ':'), 6, 0, ':') 'run_time',
        STUFF(STUFF(STUFF(RIGHT(REPLICATE('0', 8) + CAST(sh.run_duration as varchar(8)), 8), 3, 0, ':'), 6, 0, ':'), 9, 0, ':') 'run_duration (DD:HH:MM:SS)  '
FROM msdb.dbo.sysjobs sj
JOIN msdb.dbo.sysjobhistory sh
ON sj.job_id = sh.job_id
```
