---
title: Sys.remote_data_archive_tables (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d71c317ef36f254f83af70b3b4a2b2428fcbfa4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32974651"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivetables"></a>Ajustar las vistas de catálogo de base de datos - sys.remote_data_archive_tables
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada tabla remota que almacena los datos de una tabla local habilitada para Stretch.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|El identificador de objeto de la tabla local habilitada para Stretch.|  
|**remote_database_id**|**int**|El identificador local generada automáticamente de la base de datos remota.|  
|**remote_table_name**|**sysname**|El nombre de la tabla en la base de datos remoto que corresponde a la tabla local habilitada para Stretch.|  
|**filter_predicate**|**nvarchar(max)**|El predicado de filtro, si la hubiera, que identifica las filas en la tabla que desea migrar. Si el valor es nulo, toda la tabla será apta para la migración.<br /><br /> Para obtener más información, consulte [Enable Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) y [seleccionar filas para migrar mediante un predicado de filtro](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).|  
|**migration_direction**|**tinyint**|La dirección en la que están actualmente están migrando los datos. Los valores disponibles son los siguientes.<br/>1 (salida)<br/>2 (entrante)|  
|**migration_direction_desc**|**nvarchar(60)**|La descripción de la dirección en la que están actualmente están migrando los datos. Los valores disponibles son los siguientes.<br/>saliente (1)<br/>entrada (2)|  
|**is_migration_paused**|**bit**|Indica si la migración está pausada actualmente.|  
|**is_reconciled**|**bit**| Indica si la tabla remota y la tabla de SQL Server están sincronizadas.<br/><br/>Cuando el valor de **is_reconciled** es 1 (true), la tabla remota y la tabla de SQL Server están sincronizados y puede ejecutar las consultas que incluyen los datos remotos.<br/><br/>Cuando el valor de **is_reconciled** es 0 (false), la tabla remota y la tabla de SQL Server no están sincronizadas. Recientemente filas migradas tienen que migrarse de nuevo. Esto sucede cuando se restaura la base de datos de Azure remota, o cuando se eliminan filas manualmente de la tabla remota. Hasta que conciliar las tablas, no se puede ejecutar las consultas que incluyen los datos remotos. Para conciliar las tablas, ejecutar [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md). |  
  
## <a name="see-also"></a>Vea también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

