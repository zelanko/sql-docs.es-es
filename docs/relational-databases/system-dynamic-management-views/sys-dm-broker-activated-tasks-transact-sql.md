---
title: Sys.dm_broker_activated_tasks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_activated_tasks
- sys.dm_broker_activated_tasks_TSQL
- dm_broker_activated_tasks
- dm_broker_activated_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_activated_tasks dynamic management view
ms.assetid: 17e6f87f-8f56-489d-9aed-216afc8ef310
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf3910b432d803ce74e0bf24d83a974072028f33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704897"
---
# <a name="sysdmbrokeractivatedtasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada procedimiento almacenado activado por Service Broker.  
 

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**spid**|**int**|Id. de la sesión del procedimiento almacenado activado. QUE ACEPTA VALORES NULL.|  
|**database_id**|**smallint**|Id. de la base de datos en la que se define la cola. QUE ACEPTA VALORES NULL.|  
|**queue_id**|**int**|Id. del objeto de la cola para el que se activó el procedimiento almacenado. QUE ACEPTA VALORES NULL.|  
|**procedure_name**|**nvarchar(650)**|Nombre del procedimiento almacenado activado. QUE ACEPTA VALORES NULL.|  
|**execute_as**|**int**|Id. del usuario con el que se ejecuta el procedimiento almacenado. QUE ACEPTA VALORES NULL.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="physical-joins"></a>Combinaciones físicas  
 ![Combinaciones de sys.dm_broker_activated_tasks](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "combinaciones de sys.dm_broker_activated_tasks")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|Uno a uno|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con Service Broker &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

