---
title: Sys.remote_data_archive_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3633612e6aa674a5cd7513c6a84ce1d77ca46a4d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47689195"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Stretch Database vistas de catálogo - sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada tabla remota que almacena los datos de una tabla local habilitada para Stretch.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|El identificador de objeto de la tabla local habilitada para Stretch.|  
|**remote_database_id**|**int**|El identificador local generado automáticamente de la base de datos remoto.|  
|**remote_table_name**|**sysname**|El nombre de la tabla en la base de datos remoto que corresponde a la tabla local habilitada para Stretch.|  
|**filter_predicate**|**nvarchar(max)**|El predicado de filtro, si la hubiera, que identifica las filas de la tabla que desea migrar. Si el valor es nulo, toda la tabla será apta para la migración.<br /><br /> Para obtener más información, consulte [habilitar Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) y [seleccionar filas para migrar mediante el uso de un predicado de filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|La dirección en la que están actualmente están migrando los datos. Los valores disponibles son las siguientes:<br/>1 (saliente)<br/>2 (entrante)|  
|**migration_direction_desc**|**nvarchar(60)**|La descripción de la dirección en la que están actualmente están migrando los datos. Los valores disponibles son las siguientes:<br/>saliente (1)<br/>entrada (2)|  
|**is_migration_paused**|**bit**|Indica si la migración está pausada actualmente.|  
|**is_reconciled**|**bit**| Indica si la tabla remota y la tabla de SQL Server están sincronizadas.<br/><br/>Cuando el valor de **is_reconciled** es 1 (true), la tabla remota y la tabla de SQL Server están sincronizadas y puede ejecutar las consultas que incluyen los datos remotos.<br/><br/>Cuando el valor de **is_reconciled** es 0 (false), la tabla remota y la tabla de SQL Server no están sincronizadas. Recientemente filas migradas tienen que migrarse de nuevo. Esto sucede cuando se restaura la base de datos de Azure remota, o elimine manualmente las filas de la tabla remota. Hasta que conciliar las tablas, no puede ejecutar las consultas que incluyen los datos remotos. Para conciliar las tablas, ejecutar [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Vea también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

