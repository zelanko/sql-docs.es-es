---
title: ALTER MATERIALIZED VIEW (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- ALTER_VIEW_TSQL
- ALTER VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], modifying
- views [SQL Server], modifying
- modifying views
- ALTER VIEW statement
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: a38b76b39a6b3887f0dc69f7451c885ee8cbd0b6
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2019
ms.locfileid: "67566567"
---
# <a name="alter-materialized-view-transact-sql-preview"></a>ALTER MATERIALIZED VIEW (Transact-SQL) (versión preliminar)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Modifica una vista materializada creada anteriormente. ALTER VIEW no afecta a desencadenadores ni procedimientos almacenados dependientes y no cambia permisos.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```
ALTER MATERIALIZED VIEW [ schema_name . ] view_name
{
      REBUILD | DISABLE
}
[;]
```  
  
## <a name="arguments"></a>Argumentos

 *schema_name*     
 Es el nombre del esquema al que pertenece la vista.  
  
 *view_name*     
 Es la vista materializada para cambiar.  
  
*REBUILD*   
Reanuda la vista materializada.

*DISABLE*   
Suspende el mantenimiento en la vista materializada mientras se mantienen los metadatos y los permisos.  Todas las consultas de la vista materializada en un estado deshabilitado se resuelven en las tablas subyacentes.
  
## <a name="permissions"></a>Permisos

Se requiere el permiso ALTER en la tabla o la vista.
  
## <a name="examples"></a>Ejemplos

Este ejemplo deshabilita una vista materializada y la pone en modo suspendido.
  
```sql
ALTER MATERIALIZED VIEW My_Indexed_View DISABLE;  
```  
  
Este ejemplo reanuda la vista materializada compilándola de nuevo.  
  
```sql
ALTER MATERIALIZED VIEW My_Indexed_View REBUILD;  
```  
  
## <a name="see-also"></a>Vea también

[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Vistas de sistema admitidas en Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instrucciones de T-SQL compatibles con Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
