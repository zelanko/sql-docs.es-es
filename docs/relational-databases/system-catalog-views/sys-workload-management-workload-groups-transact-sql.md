---
title: Sys. workload_management_workload_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 76b5b09a07189db127c970e75dac2894fdbea1ae
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633449"
---
# <a name="sysworkload_management_workload_groups-transact-sql"></a>Sys. workload_management_workload_groups (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 Devuelve los detalles de los grupos de cargas de trabajo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|group_id|**int**|Id. único del grupo de cargas de trabajo. No admite valores NULL.||
|name|**sysname**|Nombre del grupo de cargas de trabajo Debe ser único para la instancia de.  No admite valores NULL.||
|importance|**nvarchar(128)**|Es la importancia relativa de una solicitud en este grupo de cargas de trabajo y entre grupos de cargas de trabajo para los recursos compartidos. No admite valores NULL.|Low, below_normal, normal (valor predeterminado), above_normal, alto||
|min_percentage_resource|**tinyint**|Cantidad garantizada de recursos para las solicitudes en el grupo de cargas de trabajo. Los recursos no se comparten con otros grupos de cargas de trabajo. No admite valores NULL.||
|cap_percentage_resource|**tinyint**|Límite máximo en la asignación de porcentaje de recursos para las solicitudes en el grupo de cargas de trabajo. Limita el número máximo de recursos asignados al nivel especificado. El intervalo permitido para el valor es de 1 a 100.||
|request_min_resource_grant_percent|**decimal (5, 2)**|Especifica la cantidad mínima de recursos asignados a una solicitud. El intervalo permitido para el valor es de 0,75 a 100.||
|request_max_resource_grant_percent |**decimal (5, 2)**|Especifica la cantidad máxima de recursos asignados a una solicitud.||
|query_execution_timeout_sec|**int**|La cantidad de tiempo de ejecución, en segundos, permitida antes de que se cancele la consulta.  Las consultas no se pueden cancelar una vez que han alcanzado la fase de devolución de la ejecución.  query_execution_timeout_sec no incluye el tiempo invertido en la cola.|
|query_wait_timeout_sec|**int**|NIVEL||
|create_time|**datetime**|Hora en que se creó el grupo de cargas de trabajo. No admite valores NULL.||
modify_time|**datetime**|Hora en que se modificó por última vez el grupo de cargas de trabajo. No admite valores NULL.||
|&nbsp;||||
  
## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="next-steps"></a>Pasos siguientes

 Para obtener una lista de todas las vistas de catálogo para SQL Data Warehouse y almacenamiento de datos paralelos, consulte [SQL Data Warehouse y las vistas de catálogo de almacenamiento de datos paralelas](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para crear un grupo de cargas de trabajo, consulte Creación de un [grupo de cargas](../../t-sql/statements/create-workload-group-transact-sql.md)de trabajo. Para obtener más información sobre la clasificación de cargas de trabajo, consulte aislamiento de la [carga de trabajo](/azure/sql-data-warehouse/sql-data-warehouse-workload-isolation)
