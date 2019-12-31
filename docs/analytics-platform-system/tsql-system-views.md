---
title: Vistas de sistema
description: Vistas del sistema para el sistema de plataforma analítica (APS) SQL Server almacenamiento de datos paralelos (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a7e6a0bda01de76787033607fbf35a0ca123ef95
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399804"
---
# <a name="system-views-for-analytics-platform-system-parallel-data-warehouse"></a>Vistas del sistema para el almacenamiento de datos paralelos de Analytics Platform System
Vistas del sistema para el sistema de plataforma analítica (APS) SQL Server almacenamiento de datos paralelos (PDW).

## <a name="parallel-data-warehouse-catalog-views"></a>Vistas de catálogo de almacenamiento de datos paralelos
* [Sys. pdw_column_distribution_properties](https://msdn.microsoft.com/library/mt204022.aspx)
* [Sys. pdw_database_mappings](https://msdn.microsoft.com/library/mt203891.aspx)
* [Sys. pdw_distributions](https://msdn.microsoft.com/library/mt203892.aspx)
* [Sys. pdw_index_mappings](https://msdn.microsoft.com/library/mt203912.aspx)
* [Sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)
* [Sys. pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)
* [Sys. pdw_nodes_column_store_dictionaries](https://msdn.microsoft.com/library/mt203902.aspx)
* [Sys. pdw_nodes_column_store_row_groups](https://msdn.microsoft.com/library/mt203880.aspx)
* [Sys. pdw_nodes_column_store_segments](https://msdn.microsoft.com/library/mt203916.aspx)
* [Sys. pdw_nodes_columns](https://msdn.microsoft.com/library/mt203881.aspx)
* [Sys. pdw_nodes_indexes](https://msdn.microsoft.com/library/mt203885.aspx)
* [Sys. pdw_nodes_partitions](https://msdn.microsoft.com/library/mt203908.aspx)
* [Sys. pdw_nodes_pdw_physical_databases](https://msdn.microsoft.com/library/mt203897.aspx)
* [Sys. pdw_nodes_tables](https://msdn.microsoft.com/library/mt203886.aspx)
* [Sys. pdw_table_distribution_properties](https://msdn.microsoft.com/library/mt203896.aspx)
* [Sys. pdw_table_mappings](https://msdn.microsoft.com/library/mt203876.aspx)

## <a name="parallel-data-warehouse-dynamic-management-views-dmvs"></a>Vistas de administración dinámica (DMV) de almacenamiento de datos paralelos
* [Sys. dm_pdw_dms_cores](https://msdn.microsoft.com/library/mt203911.aspx)
* [Sys. dm_pdw_dms_external_work](../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-external-work-transact-sql.md)
* [Sys. dm_pdw_dms_workers](https://msdn.microsoft.com/library/mt203878.aspx)
* [Sys. dm_pdw_errors](https://msdn.microsoft.com/library/mt203904.aspx)
* [Sys. dm_pdw_exec_connections](https://msdn.microsoft.com/library/mt203882.aspx)
* [Sys. dm_pdw_exec_requests](https://msdn.microsoft.com/library/mt203887.aspx)
* [Sys. dm_pdw_exec_sessions](https://msdn.microsoft.com/library/mt203883.aspx)
* [Sys. dm_pdw_hadoop_operations](../relational-databases/system-dynamic-management-views/sys-dm-pdw-hadoop-operations-transact-sql.md)
* [Sys. dm_pdw_lock_waits](https://msdn.microsoft.com/library/mt203901.aspx)
* [Sys. dm_pdw_nodes](https://msdn.microsoft.com/library/mt203907.aspx)
* [Sys. dm_pdw_nodes_database_encryption_keys](https://msdn.microsoft.com/library/mt203922.aspx)
* [Sys. dm_pdw_os_threads](https://msdn.microsoft.com/library/mt203917.aspx)
* [Sys. dm_pdw_request_steps](https://msdn.microsoft.com/library/mt203913.aspx)
* [Sys. dm_pdw_resource_waits](https://msdn.microsoft.com/library/mt203906.aspx)
* [Sys. dm_pdw_sql_requests](https://msdn.microsoft.com/library/mt203889.aspx)
* [Sys. dm_pdw_sys_info](https://msdn.microsoft.com/library/mt203900.aspx)
* [Sys. dm_pdw_wait_stats](https://msdn.microsoft.com/library/mt203909.aspx)
* [Sys. dm_pdw_waits](https://msdn.microsoft.com/library/mt203909.aspx)

## <a name="sql-server-dmvs-applicable-to-parallel-data-warehouse"></a>SQL Server DMV aplicables al almacenamiento de datos paralelos
Las DMV siguientes se aplican al almacenamiento de datos paralelos, pero se deben ejecutar conectándose a la base de datos **maestra** .

* [Sys. database_service_objectives](../relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database.md)
* [Sys. dm_operation_status](../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)
* [Sys. fn_helpcollations ()](../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)

## <a name="sql-server-catalog-views"></a>Vistas de catálogo de SQL Server
* [Sys. all_columns](https://msdn.microsoft.com/library/ms177522.aspx)
* [Sys. all_objects](https://msdn.microsoft.com/library/ms178618.aspx)
* [Sys. all_parameters](https://msdn.microsoft.com/library/ms190340.aspx)
* [Sys. all_sql_modules](https://msdn.microsoft.com/library/ms184389.aspx)
* [Sys. all_views](https://msdn.microsoft.com/library/ms189510.aspx)
* [Sys. Assemblies](https://msdn.microsoft.com/library/ms189790.aspx)
* [Sys. assembly_modules](https://msdn.microsoft.com/library/ms180052.aspx)
* [Sys. assembly_types](https://msdn.microsoft.com/library/ms178020.aspx)
* [Sys. Certificates](https://msdn.microsoft.com/library/ms189774.aspx)
* [Sys. check_constraints](https://msdn.microsoft.com/library/ms187388.aspx)
* [Sys. Columns](https://msdn.microsoft.com/library/ms176106.aspx)
* [Sys. computed_columns](https://msdn.microsoft.com/library/ms188744.aspx)
* [Sys. Credentials](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)
* [Sys. data_spaces](https://msdn.microsoft.com/library/ms190289.aspx)
* [Sys. database_credentials](../relational-databases/system-catalog-views/sys-database-credentials-transact-sql.md)
* [Sys. database_files](https://msdn.microsoft.com/library/ms174397.aspx)
* [Sys. database_permissions](https://msdn.microsoft.com/library/ms188367.aspx)
* [Sys. database_principals](https://msdn.microsoft.com/library/ms187328.aspx)
* [Sys. database_role_members](https://msdn.microsoft.com/library/ms189780.aspx)
* [Sys. Databases](https://msdn.microsoft.com/library/ms178534.aspx)
* [Sys. default_constraints](https://msdn.microsoft.com/library/ms173758.aspx)
* [Sys. external_data_sources](https://msdn.microsoft.com/library/dn935019.aspx)
* [Sys. external_file_formats](https://msdn.microsoft.com/library/dn935025.aspx)
* [Sys. external_tables](https://msdn.microsoft.com/library/dn935029.aspx)
* [Sys. grupos de archivos](https://msdn.microsoft.com/library/ms187782.aspx)
* [Sys. foreign_key_columns](https://msdn.microsoft.com/library/ms186306.aspx)
* [Sys. foreign_keys](https://msdn.microsoft.com/library/ms189807.aspx)
* [Sys. identity_columns](https://msdn.microsoft.com/library/ms187334.aspx)
* [Sys. index_columns](https://msdn.microsoft.com/library/ms175105.aspx)
* [Sys. Indexes](https://msdn.microsoft.com/library/ms173760.aspx)
* [Sys. key_constraints](https://msdn.microsoft.com/library/ms174321.aspx)
* [Sys. numbered_procedures](https://msdn.microsoft.com/library/ms179865.aspx)
* [Sys. Objects](https://msdn.microsoft.com/library/ms190324.aspx)
* [Sys. Parameters](https://msdn.microsoft.com/library/ms176074.aspx)
* [Sys. partition_functions](https://msdn.microsoft.com/library/ms187381.aspx)
* [Sys. partition_parameters](https://msdn.microsoft.com/library/ms175054.aspx)
* [Sys. partition_range_values](https://msdn.microsoft.com/library/ms187780.aspx)
* [Sys. partition_schemes](https://msdn.microsoft.com/library/ms189752.aspx)
* [Sys. partitions](https://msdn.microsoft.com/library/ms175012.aspx)
* [Sys. Procedures](https://msdn.microsoft.com/library/ms188737.aspx)
* [Sys. Schemas](https://msdn.microsoft.com/library/ms176011.aspx)
* [Sys. securable_classes](https://msdn.microsoft.com/library/ms408301.aspx)
* [Sys. sql_expression_dependencies](https://msdn.microsoft.com/library/bb677315.aspx)
* [Sys. sql_modules](https://msdn.microsoft.com/library/ms175081.aspx)
* [Sys. stats](https://msdn.microsoft.com/library/ms177623.aspx)
* [Sys. stats_columns](https://msdn.microsoft.com/library/ms187340.aspx)
* [Sys. symmetric_keys](../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)
* [Sys. sinónimos](../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)
* [Sys. syscharsets](../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)
* [Sys. syscolumns](../relational-databases/system-compatibility-views/sys-syscolumns-transact-sql.md)
* [Sys. sysdatabases](../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)
* [Sys. syslanguages](../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)
* [Sys. sysobjects](../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md)
* [Sys. sysreferences](../relational-databases/system-compatibility-views/sys-sysreferences-transact-sql.md)
* [Sys. system_columns](https://msdn.microsoft.com/library/ms178596.aspx)
* [Sys. system_objects](https://msdn.microsoft.com/library/ms173551.aspx)
* [Sys. system_parameters](../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)
* [Sys. system_sql_modules](https://msdn.microsoft.com/library/ms188034.aspx)
* [Sys. system_views](https://msdn.microsoft.com/library/ms187764.aspx)
* [Sys. systypes](../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)
* [Sys. sysusers](../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)
* [Sys. Tables](https://msdn.microsoft.com/library/ms187406.aspx)
* [Sys. Types](https://msdn.microsoft.com/library/ms188021.aspx)
* [Sys. views](https://msdn.microsoft.com/library/ms190334.aspx)

## <a name="sql-server-dmvs-available-in-parallel-data-warehouse"></a>SQL Server DMV disponibles en almacenamiento de datos paralelos
El almacenamiento de datos paralelos expone muchas de las vistas de administración dinámica (DMV) de SQL Server. Estas vistas, cuando se consultan en el almacenamiento de datos paralelo, informan del estado de las bases de datos de SQL Server que se ejecutan en las distribuciones.

Cada una de estas DMV tiene una columna específica denominada pdw_node_id. Este es el identificador del nodo de proceso. 

> [!NOTE]
> Para utilizar estas vistas, inserte ' pdw_nodes_ ' en el nombre, tal como se muestra en la tabla siguiente.
> 
> 

| Nombre DMV en almacenamiento de datos paralelos | Vínculo a SQL Server tema T-SQL |
|:--- |:--- |
| sys.dm_pdw_nodes_db_file_space_usage |[Sys. dm_db_file_space_usage](https://msdn.microsoft.com/library/ms174412.aspx) |
| sys.dm_pdw_nodes_db_index_usage_stats |[Sys. dm_db_index_usage_stats](https://msdn.microsoft.com/library/ms188755.aspx) |
| sys.dm_pdw_nodes_db_partition_stats |[Sys. dm_db_partition_stats](https://msdn.microsoft.com/library/ms187737.aspx) |
| sys.dm_pdw_nodes_db_session_space_usage |[Sys. dm_db_session_space_usage](https://msdn.microsoft.com/library/ms187938.aspx) |
| sys.dm_pdw_nodes_db_task_space_usage |[Sys. dm_db_task_space_usage](https://msdn.microsoft.com/library/ms190288.aspx) |
| sys.dm_pdw_nodes_exec_background_job_queue |[Sys. dm_exec_background_job_queue](https://msdn.microsoft.com/library/ms173512.aspx) |
| sys.dm_pdw_nodes_exec_background_job_queue_stats |[Sys. dm_exec_background_job_queue_stats](https://msdn.microsoft.com/library/ms176059.aspx) |
| sys.dm_pdw_nodes_exec_cached_plans |[Sys. dm_exec_cached_plans](https://msdn.microsoft.com/library/ms187404.aspx) |
| sys.dm_pdw_nodes_exec_connections |[Sys. dm_exec_connections](https://msdn.microsoft.com/library/ms181509.aspx) |
| sys.dm_pdw_nodes_exec_procedure_stats |[Sys. dm_exec_procedure_stats](https://msdn.microsoft.com/library/cc280701.aspx) |
| sys.dm_pdw_nodes_exec_query_memory_grants |[Sys. dm_exec_query_memory_grants](https://msdn.microsoft.com/library/ms365393.aspx) |
| sys.dm_pdw_nodes_exec_query_optimizer_info |[Sys. dm_exec_query_optimizer_info](https://msdn.microsoft.com/library/ms175002.aspx) |
| sys.dm_pdw_nodes_exec_query_resource_semaphores |[Sys. dm_exec_query_resource_semaphores](https://msdn.microsoft.com/library/ms366321.aspx) |
| sys.dm_pdw_nodes_exec_query_stats |[Sys. dm_exec_query_stats](https://msdn.microsoft.com/library/ms189741.aspx) |
| sys.dm_pdw_nodes_exec_requests |[Sys. dm_exec_requests](https://msdn.microsoft.com/library/ms177648.aspx) |
| sys.dm_pdw_nodes_exec_sessions |[Sys. dm_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) |
| sys.dm_pdw_nodes_io_pending_io_requests |[Sys. dm_io_pending_io_requests](https://msdn.microsoft.com/library/ms188762.aspx) |
| sys.dm_pdw_nodes_os_buffer_descriptors |[Sys. dm_os_buffer_descriptors](https://msdn.microsoft.com/library/ms173442.aspx) |
| sys.dm_pdw_nodes_os_child_instances |[Sys. dm_os_child_instances](https://msdn.microsoft.com/library/ms165698.aspx) |
| sys.dm_pdw_nodes_os_cluster_nodes |[Sys. dm_os_cluster_nodes](https://msdn.microsoft.com/library/ms187341.aspx) |
| sys.dm_pdw_nodes_os_dispatcher_pools |[Sys. dm_os_dispatcher_pools](https://msdn.microsoft.com/library/bb630336.aspx) |
| sys.dm_pdw_nodes_os_dispatchers |La documentación de Transact-SQL no está disponible. |
| sys.dm_pdw_nodes_os_hosts |[Sys. dm_os_hosts](https://msdn.microsoft.com/library/ms187800.aspx) |
| sys.dm_pdw_nodes_os_latch_stats |[Sys. dm_os_latch_stats](https://msdn.microsoft.com/library/ms175066.aspx) |
| sys.dm_pdw_nodes_os_memory_brokers |[Sys. dm_os_memory_brokers](https://msdn.microsoft.com/library/bb522548.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_clock_hands |[Sys. dm_os_memory_cache_clock_hands](https://msdn.microsoft.com/library/ms173786.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_counters |[Sys. dm_os_memory_cache_counters](https://msdn.microsoft.com/library/ms188760.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_entries |[Sys. dm_os_memory_cache_entries](https://msdn.microsoft.com/library/ms189488.aspx) |
| sys.dm_pdw_nodes_os_memory_cache_hash_tables |[Sys. dm_os_memory_cache_hash_tables](https://msdn.microsoft.com/library/ms182388.aspx) |
| sys.dm_pdw_nodes_os_memory_clerks |[Sys. dm_os_memory_clerks](https://msdn.microsoft.com/library/ms175019.aspx) |
| sys.dm_pdw_nodes_os_memory_node_access_stats |La documentación de Transact-SQL no está disponible. |
| sys.dm_pdw_nodes_os_memory_nodes |[Sys. dm_os_memory_nodes](https://msdn.microsoft.com/library/bb510622.aspx) |
| sys.dm_pdw_nodes_os_memory_objects |[Sys. dm_os_memory_objects](../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) |
| sys.dm_pdw_nodes_os_memory_pools |[Sys. dm_os_memory_pools](https://msdn.microsoft.com/library/ms175022.aspx) |
| sys.dm_pdw_nodes_os_nodes |[Sys. dm_os_nodes](https://msdn.microsoft.com/library/bb510628.aspx) |
| sys.dm_pdw_nodes_os_performance_counters |[Sys. dm_os_performance_counters](https://msdn.microsoft.com/library/ms187743.aspx) |
| sys.dm_pdw_nodes_os_process_memory |[Sys. dm_os_process_memory](https://msdn.microsoft.com/library/bb510747.aspx) |
| sys.dm_pdw_nodes_os_schedulers |[Sys. dm_os_schedulers](https://msdn.microsoft.com/library/ms177526.aspx) |
| sys.dm_pdw_nodes_os_spinlock_stats |La documentación de Transact-SQL no está disponible. |
| sys.dm_pdw_nodes_os_sys_info |[Sys. dm_os_sys_info](https://msdn.microsoft.com/library/ms175048.aspx) |
| sys.dm_pdw_nodes_os_sys_memory |[Sys. dm_os_memory_nodes](https://msdn.microsoft.com/library/bb510622.aspx) |
| sys.dm_pdw_nodes_os_tasks |[Sys. dm_os_tasks](https://msdn.microsoft.com/library/ms174963.aspx) |
| sys.dm_pdw_nodes_os_threads |[Sys. dm_os_threads](https://msdn.microsoft.com/library/ms187818.aspx) |
| sys.dm_pdw_nodes_os_virtual_address_dump |[Sys. dm_os_virtual_address_dump](../relational-databases/system-dynamic-management-views/sys-dm-os-virtual-address-dump-transact-sql.md) |
| sys.dm_pdw_nodes_os_wait_stats |[Sys. dm_os_wait_stats](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md) |
| sys.dm_pdw_nodes_os_waiting_tasks |[Sys. dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md) |
| sys.dm_pdw_nodes_os_workers |[Sys. dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md) |
| sys.dm_pdw_nodes_resource_governor_resource_pools |[Sys. dm_resource_governor_resource_pools](https://msdn.microsoft.com/library/bb934023.aspx) |
| sys.dm_pdw_nodes_resource_governor_workload_groups |[Sys. dm_resource_governor_workload_groups](https://msdn.microsoft.com/library/bb934197.aspx) |
| sys.dm_pdw_nodes_tran_active_snapshot_database_transactions |[Sys. dm_tran_active_snapshot_database_transactions](https://msdn.microsoft.com/library/ms180023.aspx) |
| sys.dm_pdw_nodes_tran_active_transactions |[Sys. dm_tran_active_transactions](https://msdn.microsoft.com/library/ms174302.aspx) |
| sys.dm_pdw_nodes_tran_commit_table |[Sys. dm_tran_commit_table](../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md) |
| sys.dm_pdw_nodes_tran_current_snapshot |[Sys. dm_tran_current_snapshot](https://msdn.microsoft.com/library/ms184390.aspx) |
| sys.dm_pdw_nodes_tran_current_transaction |[Sys. dm_tran_current_transaction](../relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql.md) |
| sys.dm_pdw_nodes_tran_database_transactions |[Sys. dm_tran_database_transactions](../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) |
| sys.dm_pdw_nodes_tran_locks |[Sys. dm_tran_locks](https://msdn.microsoft.com/library/ms190345.aspx) |
| sys.dm_pdw_nodes_tran_session_transactions |[Sys. dm_tran_session_transactions](https://msdn.microsoft.com/library/ms188739.aspx) |
| sys.dm_pdw_nodes_tran_top_version_generators |[Sys. dm_tran_top_version_generators](https://msdn.microsoft.com/library/ms188778.aspx) |

## <a name="sql-server-2016-polybase-dmvs-available-in-parallel-data-warehouse"></a>SQL Server las DMV de polybase 2016 disponibles en almacenamiento de datos paralelos
* [Sys. dm_exec_compute_node_errors](https://msdn.microsoft.com/library/mt146380.aspx)
* [Sys. dm_exec_compute_node_status](https://msdn.microsoft.com/library/mt146382.aspx)
* [Sys. dm_exec_compute_nodes](../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)
* [Sys. dm_exec_distributed_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-exec-distributed-request-steps-transact-sql.md)
* [Sys. dm_exec_distributed_requests](https://msdn.microsoft.com/library/mt146385.aspx)
* [Sys. dm_exec_distributed_sql_requests](https://msdn.microsoft.com/library/mt146390.aspx)
* [Sys. dm_exec_dms_services](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-services-transact-sql.md)
* [Sys. dm_exec_dms_workers](../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)
* [Sys. dm_exec_external_operations](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-operations-transact-sql.md)
* [Sys. dm_exec_external_work](../relational-databases/system-dynamic-management-views/sys-dm-exec-external-work-transact-sql.md)

## <a name="sql-server-information_schema-views"></a>Vistas INFORMATION_SCHEMA de SQL Server
* [CHECK_CONSTRAINTS](../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)
* [COLUMNAS](../relational-databases/system-information-schema-views/columns-transact-sql.md)
* [PARÁMETROS](../relational-databases/system-information-schema-views/parameters-transact-sql.md)
* [RUTINAS](../relational-databases/system-information-schema-views/routines-transact-sql.md)
* [SCHEMATA](../relational-databases/system-information-schema-views/schemata-transact-sql.md)
* [TABLAS](../relational-databases/system-information-schema-views/tables-transact-sql.md)
* [VIEW_COLUMN_USAGE](../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)
* [VIEW_TABLE_USAGE](../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)
* [Vistas](../relational-databases/system-information-schema-views/views-transact-sql.md)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información de referencia, vea [elementos del lenguaje t-SQL](tsql-language-elements.md) e [instrucciones t-SQL](tsql-statements.md).

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse reference overview]: sql-data-warehouse-overview-reference.md

<!--MSDN references-->


<!--Other Web references-->
