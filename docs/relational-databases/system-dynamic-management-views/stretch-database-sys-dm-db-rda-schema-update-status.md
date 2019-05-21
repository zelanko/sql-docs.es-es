---
title: sys.dm_db_rda_schema_update_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 85c12ae224203def43c9f9953cada0c336e9ebbd
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65947384"
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database - sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada tarea de actualización de esquema para el archivo de datos remotos de cada tabla habilitada para Stretch en la base de datos actual. Las tareas se identifican por sus identificadores de tarea.  
  
 **dm_db_rda_schema_update_status** tiene como ámbito el contexto de base de datos actual. Asegúrese de que se encuentra en el contexto de base de datos de la tabla habilitada para Stretch para la que desea ver el estado de actualización de esquema.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|Se está actualizando el identificador de la tabla local habilitada para Stretch esquema de archivo de cuyos datos remotos.|  
|**database_id**|**int**|El identificador de la base de datos que contiene la tabla habilitada para Stretch local.|  
|**task_id**|**bigint**|El identificador de la tarea de actualización de esquema de archivo de datos remotos.|  
|**task_type**|**int**|El tipo de la tarea de actualización de esquema de archivo de datos remotos.|  
|**task_type_desc**|**nvarchar**|La descripción del tipo de la tarea de actualización de esquema de archivo de datos remotos.|  
|**task_state**|**int**|El estado de la tarea de actualización de esquema de archivo de datos remotos.|  
|**task_state_des**|**nvarchar**|La descripción del estado de la tarea de actualización de esquema de archivo de datos remotos.|  
|**start_time_utc**|**datetime**|La hora UTC a la que inició la actualización del esquema de archivo de los datos remotos.|  
|**end_time_utc**|**datetime**|Ha finalizado la hora UTC en que los datos remotos archivar la actualización del esquema.|  
|**error_number**|**int**|Si se produce un error en la actualización del esquema de archivo de datos remoto, el número de error del error producido; en caso contrario, es null.|  
|**error_severity**|**int**|Si se produce un error en la actualización del esquema de archivo de datos remotos, la gravedad del error producido; en caso contrario, es null.|  
|**error_state**|**int**|Si se produce un error en la actualización del esquema de archivo de datos remoto, el estado del error producido; en caso contrario, es null. El error_state indica la condición o la ubicación donde se produjo el error.|  
  
## <a name="see-also"></a>Vea también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
