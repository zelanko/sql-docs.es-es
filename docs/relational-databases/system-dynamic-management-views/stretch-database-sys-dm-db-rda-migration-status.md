---
title: Sys. dm_db_rda_migration_status (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_migration_status
- sys.dm_db_rda_migration_status_TSQL
- dm_db_rda_migration_status
- dm_db_rda_migration_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_rda_migration_status dynamic management view
ms.assetid: faf3901c-a0e0-4e0c-8b1b-86d9f15f34dd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 1e383b01ce40dbb03f5134bf5374b9b39bc2a99e
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053495"
---
# <a name="stretch-database---sysdm_db_rda_migration_status"></a>Stretch Database-sys. dm_db_rda_migration_status
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Contiene una fila por cada lote de datos migrados de cada tabla habilitada para stretch en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los lotes se identifican por su hora de inicio y de finalización.  
  
 **Sys. dm_db_rda_migration_status** está en el ámbito del contexto de la base de datos actual. Asegúrese de que se encuentra en el contexto de la base de datos de las tablas habilitadas para stretch para los que desea ver el estado de la migración.  
  
 En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] , la salida de **sys. dm_db_rda_migration_status** está limitada a 200 filas.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|IDENTIFICADOR de la tabla desde la que se migraron las filas.|  
|**database_id**|**int**|IDENTIFICADOR de la base de datos desde la que se migraron las filas.|  
|**migrated_rows**|**bigint**|Número de filas migradas en este lote.|  
|**start_time_utc**|**datetime**|Hora UTC a la que se inició el lote.|  
|**end_time_utc**|**datetime**|Hora UTC a la que finalizó el lote.|  
|**error_number**|**int**|Si se produce un error en el lote, el número de error del error que se produjo; de lo contrario, es NULL.|  
|**error_severity**|**int**|Si se produce un error en el lote, la gravedad del error que se produjo; de lo contrario, es NULL.|  
|**error_state**|**int**|Si se produce un error en el lote, el estado del error que se produjo; de lo contrario, es NULL.<br /><br /> El **error_state** indica la condición o la ubicación donde se produjo el error.|  
  
## <a name="see-also"></a>Consulte también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
