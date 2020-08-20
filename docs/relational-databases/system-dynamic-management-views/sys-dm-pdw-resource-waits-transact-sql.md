---
description: Sys. dm_pdw_resource_waits (Transact-SQL)
title: Sys. dm_pdw_resource_waits (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/26/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a43ce9a2-5261-41e3-97f0-555ba05ebed9
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: cf3b21433a4eb19be526487e9df03a8df7bce276
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474700"
---
# <a name="sysdm_pdw_resource_waits-transact-sql"></a>Sys. dm_pdw_resource_waits (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Muestra información de espera para todos los tipos de recursos de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|wait_id|**bigint**|Posición de la solicitud en la lista de espera.|ordinal basado en 0. Esto no es único en todas las entradas de espera.|  
|session_id|**nvarchar(32)**|IDENTIFICADOR de la sesión en la que se ha producido el estado de espera.|Vea session_id en [Sys. dm_pdw_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).|  
|type|**nvarchar(255)**|Tipo de espera que esta entrada representa.|Valores posibles:<br /><br /> Conexión<br /><br /> Simultaneidad de consultas locales<br /><br /> Simultaneidad de consultas distribuidas<br /><br /> Simultaneidad de DMS<br /><br /> Simultaneidad de copias de seguridad|  
|object_type|**nvarchar(255)**|Tipo de objeto que se ve afectado por la espera.|Valores posibles:<br /><br /> **OBJETO**<br /><br /> **BASE**<br /><br /> **INTEGRADO**<br /><br /> **ESQUEMA**<br /><br /> **APLICACIÓN**|  
|object_name|**nvarchar (386)**|Nombre o GUID del objeto especificado que se ha visto afectado por la espera.|Las tablas y vistas se muestran con nombres de tres partes.<br /><br /> Los índices y las estadísticas se muestran con nombres de cuatro partes.<br /><br /> Los nombres, entidades de seguridad y bases de datos son nombres de cadena.|  
|request_id|**nvarchar(32)**|IDENTIFICADOR de la solicitud en la que se produjo el estado de espera.|Identificador de QID de la solicitud.<br /><br /> Identificador GUID para las solicitudes de carga.|  
|request_time|**datetime**|Hora a la que se solicitó el bloqueo o el recurso.||  
|acquire_time|**datetime**|Hora a la que se adquirió el bloqueo o el recurso.||  
|state|**nvarchar(50)**|Estado del estado de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|priority|**int**|Prioridad del elemento de espera.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|concurrency_slots_used|**int**|Interno|Vea las [esperas de recursos de monitor](#monitor-resource-waits) a continuación|  
|resource_class|**nvarchar (20)**|Interno |Vea las [esperas de recursos de monitor](#monitor-resource-waits) a continuación|  
  
## <a name="monitor-resource-waits"></a>Supervisar esperas de recursos 
Con la introducción de [grupos de cargas de trabajo](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation), los espacios de simultaneidad ya no son aplicables.  Utilice la consulta siguiente y la `resources_requested` columna para comprender los recursos necesarios para ejecutar la solicitud.

```sql
select rw.wait_id
      ,rw.session_id
      ,rw.type
      ,rw.object_type
      ,rw.object_name
      ,rw.request_id
      ,rw.request_time
      ,rw.acquire_time
      ,rw.state
      ,resources_requested = s.effective_request_min_resource_grant_percent
      ,r.group_name
  from sys.dm_workload_management_workload_groups_stats s
  join sys.dm_pdw_exec_requests r on r.group_name = s.name collate SQL_Latin1_General_CP1_CI_AS
  join sys.dm_pdw_resource_waits rw on rw.request_id = r.request_id
```

## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
