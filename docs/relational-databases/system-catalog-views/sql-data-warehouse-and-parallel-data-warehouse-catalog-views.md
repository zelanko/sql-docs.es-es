---
description: Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos
title: Vistas de catálogo
titleSuffix: Azure SQL Data Warehouse and Parallel Data Warehouse
ms.date: 10/29/2019
ms.service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: ef6f58e2-0162-4bb2-951a-a786da7453e4
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: 8682f7d5549389ff98d20862ce86f6d177b3116e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486520"
---
# <a name="sql-data-warehouse-and-parallel-data-warehouse-catalog-views"></a>Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

 En este tema se enumeran las [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] vistas de catálogo y.  
  
## <a name="sssdw-and-sspdw-catalog-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] vistas de catálogo  
 Las siguientes vistas de catálogo se aplican tanto a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] como a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] :  
  
 [Sys. pdw_column_distribution_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-column-distribution-properties-transact-sql.md)  
  
 [Sys. pdw_distributions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-distributions-transact-sql.md)  
  
 [Sys. pdw_index_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)  
  
 [sys.pdw_loader_backup_run_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
 [sys.pdw_loader_backup_runs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
 [Sys. pdw_nodes_column_store_dictionaries &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-dictionaries-transact-sql.md)  
  
 [Sys. pdw_nodes_column_store_row_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-row-groups-transact-sql.md)  
  
 [Sys. pdw_nodes_column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-column-store-segments-transact-sql.md)  
  
 [Sys. pdw_nodes_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-columns-transact-sql.md)  
  
 [Sys. pdw_nodes_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-indexes-transact-sql.md)  
  
 [Sys. pdw_nodes_partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-partitions-transact-sql.md)  
  
 [Sys. pdw_nodes_pdw_physical_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
 [Sys. pdw_nodes_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-tables-transact-sql.md) 

 [sys.pdw_replicated_table_cache_state (Transact-SQL)](sys-pdw-replicated-table-cache-state-transact-sql.md) 
  
 [Sys. pdw_table_distribution_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-distribution-properties-transact-sql.md)  
  
 [Sys. pdw_table_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md) 

## <a name="sssdw-catalog-views"></a>[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Vistas de catálogo

 Las siguientes vistas de catálogo solo se aplican a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] :

 [sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest) 

 [sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest) 

 [Sys. pdw_materialized_view_mappings &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest) (versión preliminar)

 [Sys. workload_management_workload_classifier_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifier-details-transact-sql.md)
  
 [Sys. workload_management_workload_classifiers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-workload-management-workload-classifiers-transact-sql.md)
  
 [Sys. workload_management_workload_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql?view=azure-sqldw-latest) 


## <a name="sspdw-catalog-views"></a>[!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Vistas de catálogo

 Las siguientes vistas de catálogo solo se aplican a [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] :

 [Sys. pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
 [Sys. pdw_diag_event_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-event-properties-transact-sql.md)  
  
 [Sys. pdw_diag_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md)  
  
 [Sys. pdw_diag_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md)  
  
 [Sys. pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md)  
  
 [Sys. pdw_health_component_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-groups-transact-sql.md)  
  
 [Sys. pdw_health_component_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-properties-transact-sql.md)  
  
 [Sys. pdw_health_component_status_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-component-status-mappings-transact-sql.md)  
  
 [Sys. pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)  
  
 [sys.pdw_loader_run_stages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
