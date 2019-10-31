---
title: Vistas de administración dinámica de SQL y almacenamiento de datos paralelos | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: e713365e-d44c-4b66-84c9-81a1bcc32414
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 481896da6b53189a7b54f2cb770b0c3a29031d37
ms.sourcegitcommit: af6f66cc3603b785a7d2d73d7338961a5c76c793
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73142740"
---
# <a name="sql-and-parallel-data-warehouse-dynamic-management-views"></a>Vistas de administración dinámica de almacenamiento de datos SQL y paralelo
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

En este tema se enumeran las vistas de administración dinámica de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] (DMV).  
  
 Todas [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] DMV comienzan con **Sys. DM _ _pdw**.  
  
## <a name="includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd-dynamic-management-views"></a>Vistas de administración dinámica [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Las siguientes vistas de administración dinámica se aplican tanto a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] como a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:  
  
 [Sys. DM _ &#40;_pdw_dms_cores TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-cores-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_dms_external_work TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_dms_workers TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_errors TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_exec_connections TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_exec_requests TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_exec_sessions TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_hadoop_operations TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_lock_waits TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-lock-waits-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_nodes TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_nodes_database_encryption_keys TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_os_threads TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-threads-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_request_steps TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_resource_waits TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-resource-waits-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_sql_requests TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sql-requests-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_sys_info TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-sys-info-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_wait_stats TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-wait-stats-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_waits TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  

## <a name="sql-data-warehouse-dynamic-management-views"></a>SQL Data Warehouse vistas de administración dinámica
[Sys. DM _ &#40;_pdw_nodes_exec_query_plan TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-plan-transact-sql.md)  

[Sys. DM _ &#40;_pdw_nodes_exec_query_profiles TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-profiles-transact-sql.md)  

[Sys. DM _ &#40;_pdw_nodes_exec_query_statistics_xml TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-query-statistics-xml-transact-sql.md)  

[Sys. DM _ _pdw_nodes_exec_sql: &#40;texto de TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-sql-text-transact-sql.md)  

[Sys. DM _ &#40;_pdw_nodes_exec_text_query_plan TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-exec-text-query-plan-transact-sql.md)  


## <a name="includesspdwincludessspdw-mdmd-dynamic-management-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] vistas de administración dinámica  
 Las siguientes vistas de administración dinámica solo se aplican a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:  
  
 [Sys. DM _ &#40;_pdw_component_health_active_alerts TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_component_health_alerts TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_component_health_status TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_diag_processing_stats TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-diag-processing-stats-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_network_credentials TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_node_status TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-node-status-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_os_event_logs TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-event-logs-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_os_performance_counters TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-os-performance-counters-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_query_stats_xe TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-transact-sql.md)  
  
 [Sys. DM _ &#40;_pdw_query_stats_xe_file TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-query-stats-xe-file-transact-sql.md)  
  
## <a name="see-also"></a>Ver también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  
