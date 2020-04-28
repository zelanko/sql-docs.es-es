---
title: Sys. remote_data_archive_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 65e42e6303b467abd38ddadb6be0c0d0fece46e5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68018190"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_tables"></a>Stretch Database vistas de catálogo: sys. remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada tabla remota que almacena datos de una tabla local habilitada para Stretch.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|IDENTIFICADOR de objeto de la tabla local habilitada para Stretch.|  
|**remote_database_id**|**int**|El identificador local generado automáticamente de la base de datos remota.|  
|**remote_table_name**|**sysname**|Nombre de la tabla de la base de datos remota que corresponde a la tabla local habilitada para Stretch.|  
|**filter_predicate**|**nvarchar(max)**|Predicado de filtro, si existe, que identifica las filas de la tabla que se va a migrar. Si el valor es null, la tabla completa es elegible para la migración.<br /><br /> Para obtener más información, vea [habilitar Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) y [seleccionar las filas que se van a migrar mediante un predicado de filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|Dirección en la que se están migrando actualmente los datos. Los valores disponibles son los siguientes.<br/>1 (saliente)<br/>2 (entrada)|  
|**migration_direction_desc**|**nvarchar(60)**|Descripción de la dirección en la que se están migrando actualmente los datos. Los valores disponibles son los siguientes.<br/>saliente (1)<br/>entrante (2)|  
|**is_migration_paused**|**bit**|Indica si la migración está en pausa actualmente.|  
|**is_reconciled**|**bit**| Indica si la tabla remota y la tabla SQL Server están sincronizadas.<br/><br/>Cuando el valor de **is_reconciled** es 1 (true), la tabla remota y la tabla SQL Server están sincronizadas y se pueden ejecutar consultas que incluyan los datos remotos.<br/><br/>Cuando el valor de **is_reconciled** es 0 (false), la tabla remota y la tabla SQL Server no están sincronizadas. Las filas migradas recientemente tienen que migrarse de nuevo. Esto sucede cuando se restaura la base de datos remota de Azure, o cuando se eliminan filas manualmente de la tabla remota. Hasta que se reconcilian las tablas, no se pueden ejecutar consultas que incluyan los datos remotos. Para conciliar las tablas, ejecute [Sys. sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Consulte también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

