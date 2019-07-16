---
title: dbo.sysjobschedules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
author: stevestein
ms.author: sstein
ms.openlocfilehash: a7f2dfc6196bfba6c274eb45a45745159447cc39
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061179"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información de programación de los trabajos que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutar. Esta tabla se almacena en el **msdb** base de datos.  
  
> **NOTA:** El **sysjobschedules** tabla actualiza cada 20 minutos, que pueden afectar a los valores devueltos por la **sp_help_jobschedule** procedimiento almacenado.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Id. de la programación.|  
|**job_id**|**uniqueidentifier**|Identificador del trabajo.|  
|**next_run_date**|**int**|La siguiente fecha programada para que se ejecute el trabajo. La fecha tiene el formato AAAAMMDD.|  
|**next_run_time**|**int**|La hora a la que está programada la ejecución del trabajo. La hora tiene el formato HHMMSS y utiliza un reloj de 24 horas.|  
  
## <a name="see-also"></a>Vea también  
 [dbo.sysschedules &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
