---
title: Sys.dm_db_rda_migration_status (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
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
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a8778c09acc143bc6384f9b82ff03fa25603334
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464311"
---
# <a name="stretch-database---sysdmdbrdamigrationstatus"></a>Stretch Database - sys.dm_db_rda_migration_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada lote de los datos migrados desde cada tabla habilitada para Stretch en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los lotes se identifican mediante su hora de inicio y la hora de finalización.  
  
 **Sys.dm_db_rda_migration_status** tiene un ámbito para el contexto de base de datos actual. Asegúrese de que se encuentra en el contexto de base de datos de las tablas de habilitar Stretch para la que desea ver el estado de la migración.  
  
 En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], la salida de **sys.dm_db_rda_migration_status** está limitada a 200 filas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|El identificador de la tabla desde la que se han migrado filas.|  
|**database_id**|**int**|El identificador de la base de datos desde el que se han migrado filas.|  
|**migrated_rows**|**bigint**|El número de filas se migra en este lote.|  
|**start_time_utc**|**datetime**|La hora UTC en que se inició el lote.|  
|**end_time_utc**|**datetime**|La hora UTC en que finalizó el lote.|  
|**error_number**|**int**|Si se produce un error en el lote, el número de error del error que se ha producido; en caso contrario, es null.|  
|**error_severity**|**int**|Si se produce un error en el lote, la gravedad del error que se ha producido; en caso contrario, es null.|  
|**error_state**|**int**|Si se produce un error en el lote, el estado del error que se ha producido; en caso contrario, es null.<br /><br /> El **error_state** indica la condición o la ubicación donde se produjo el error.|  
  
## <a name="see-also"></a>Vea también  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
