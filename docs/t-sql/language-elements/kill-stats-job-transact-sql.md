---
title: KILL STATS JOB (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f1738c96709d2eb1489c9ec25c598459842e3ab
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Finaliza un trabajo de actualización de estadísticas asincrónico en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
KILL STATS JOB job_id   
```  
  
## <a name="arguments"></a>Argumentos  
 *job_id*  
 Es el campo job_id devuelto por la vista de administración dinámica sys.dm_exec_background_job_queue del trabajo.  
  
## <a name="remarks"></a>Comentarios  
 job_id no guarda relación con session_id ni con la unidad de trabajo utilizada en otras formas de la instrucción KILL.  
  
## <a name="permissions"></a>Permissions  
 El usuario debe disponer del permiso VIEW SERVER STATE para tener acceso a la información desde la vista de administración dinámica sys.dm_exec_background_job_queue.  
  
 De forma predeterminada, los permisos KILL STATS JOB corresponden a los miembros de los roles fijos de base de datos sysadmin y processadmin, y estos permisos no se pueden transferir.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo finalizar la actualización de estadísticas asociada con un trabajo donde el *job_id* = `53`.  
  
```  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [KILL &#40; Transact-SQL &#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [Eliminar suscripción de notificación de consulta &#40; Transact-SQL &#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [Sys.dm_exec_background_job_queue &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [Estadísticas](../../relational-databases/statistics/statistics.md)  
  
  

