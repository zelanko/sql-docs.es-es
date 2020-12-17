---
description: sys.pdw_materialized_view_column_distribution_properties (Transact-SQL)
title: sys.pdw_materialized_view_column_distribution_properties (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 474641017502e6a3c70550285e333a00e5386475
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/17/2020
ms.locfileid: "97642889"
---
# <a name="syspdw_materialized_view_column_distribution_properties-transact-sql"></a>sys.pdw_materialized_view_column_distribution_properties (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Muestra información de distribución para las columnas de una vista materializada.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**int**|IDENTIFICADOR del objeto al que pertenece la columna. |  
|column_id|**int**|IDENTIFICADOR de la columna.|  
|distribution_ordinal|**tinyint**|0 = no es una columna de distribución.</br> 1 = Azure Synapse Analytics usa esta columna para distribuir la vista materializada.|
 
## <a name="permissions"></a>Permisos 

Necesita el permiso VIEW DATABASE STATE.

## <a name="see-also"></a>Consulte también

[Optimización del rendimiento con vista materializada](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-materialized-view-as-select-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-materialized-view-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[EXPLAIN &#40;Transact-SQL&#41;](../../t-sql/queries/explain-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-mappings-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[Vistas de catálogo de Azure Synapse Analytics y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Vistas del sistema admitidas en Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instrucciones T-SQL admitidas en Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)