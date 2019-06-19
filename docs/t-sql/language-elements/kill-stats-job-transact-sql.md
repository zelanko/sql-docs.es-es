---
title: KILL STATS JOB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c2a2a034348df16f7ea1f326d78322f578953757
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65982131"
---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Finaliza un trabajo de actualización de estadísticas asincrónico en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>Argumentos  
 *job_id*  
 Es el campo job_id devuelto por la vista de administración dinámica sys.dm_exec_background_job_queue del trabajo.  
  
## <a name="remarks"></a>Notas  
 job_id no guarda relación con session_id ni con la unidad de trabajo utilizada en otras formas de la instrucción KILL.  
  
## <a name="permissions"></a>Permisos  
 El usuario debe disponer del permiso VIEW SERVER STATE para tener acceso a la información desde la vista de administración dinámica sys.dm_exec_background_job_queue.  
  
 De forma predeterminada, los permisos KILL STATS JOB corresponden a los miembros de los roles fijos de base de datos sysadmin y processadmin, y estos permisos no se pueden transferir.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo finalizar la actualización de estadísticas asociada a un trabajo donde *job_id* = `53`.  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [Estadísticas](../../relational-databases/statistics/statistics.md)  
  
  
