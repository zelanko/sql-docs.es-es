---
description: dbo.sysjobschedules (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2cd3180f982b978a5918b505f9cf0989baf4e0fa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544599"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene información de programación de los trabajos que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutar. Esta tabla se almacena en la base de datos **msdb** .  
  
> **Nota:** La tabla **sysjobschedules** se actualiza cada 20 minutos, lo que puede afectar a los valores devueltos por la **sp_help_jobschedule** procedimiento almacenado.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Id. de la programación.|  
|**job_id**|**uniqueidentifier**|IDENTIFICADOR del trabajo.|  
|**next_run_date**|**int**|La siguiente fecha programada para que se ejecute el trabajo. La fecha tiene el formato AAAAMMDD.|  
|**next_run_time**|**int**|La hora a la que está programada la ejecución del trabajo. La hora tiene el formato HHMMSS y utiliza un reloj de 24 horas.|  
  
## <a name="see-also"></a>Consulte también  
 [ Programaciones dedbo.sys&#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
