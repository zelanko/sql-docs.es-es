---
title: Vistas de catálogo de almacenamiento de datos en paralelo y SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ef6f58e2-0162-4bb2-951a-a786da7453e4
aauthor: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e4e84dc262cd03de74433c2e713b3a7b4cda0faa
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583289"
---
# <a name="sql-data-warehouse-and-parallel-data-warehouse-catalog-views"></a>SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 Este tema se enumeran los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] vistas de catálogo.  
  
 Todos los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] vistas de catálogo comienzan con **sys.pdw**.  
  
## <a name="includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd-catalog-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] vistas de catálogo  
 Las vistas de catálogo siguientes se aplican a ambos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:  
  
 [sys.pdw_column_distribution_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md)  
  
 [sys.pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)  
  
 [sys.pdw_index_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
 [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
 [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
 [sys.pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)  
  
 [sys.pdw_nodes_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md)  
  
 [sys.pdw_nodes_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md)  
  
 [sys.pdw_nodes_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md)  
  
 [sys.pdw_nodes_pdw_physical_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
 [sys.pdw_nodes_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md) 

 [sys.pdw_replicated_table_cache_state (Transact-SQL)](sys-pdw-replicated-table-cache-state-transact-sql.md) 
  
 [sys.pdw_table_distribution_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md)  
  
 [sys.pdw_table_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md) 

[sys.workload_management_workload_classifier_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md) (Preview)

[sys.workload_management_workload_classifiers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md) (Preview)

> [!Note]
> Clasificación de la carga de trabajo está disponible para vista previa en SQL Data Warehouse Gen2. Clasificación de la administración de cargas de trabajo y la importancia de vista previa es para las compilaciones con una fecha de lanzamiento de 9 de abril de 2019 o posterior.  Los usuarios deben evitar usar compilaciones anteriores a esta fecha para pruebas de carga de trabajo administración.  Para determinar si la compilación es capaz de administración de cargas de trabajo, ejecutar select @@version cuando se conecta a la instancia de SQL Data Warehouse.
 
## <a name="includesspdwincludessspdw-mdmd-catalog-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Vistas de catálogo  
 Las vistas de catálogo siguientes se aplican a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] solo:

 [sys.pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
 [sys.pdw_diag_event_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-event-properties-transact-sql.md)  
  
 [sys.pdw_diag_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md)  
  
 [sys.pdw_diag_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md)  
  
 [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)  
  
 [sys.pdw_health_component_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)  
  
 [sys.pdw_health_component_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)  
  
 [sys.pdw_health_component_status_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)  
  
 [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)  
  
 [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
