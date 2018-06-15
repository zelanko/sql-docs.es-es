---
title: restorefile (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- restorefile
- restorefile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorefile system table
- restoring files [SQL Server], restorefile system table
- file restores [SQL Server], restorefile system table
ms.assetid: 8e40145a-8559-4abe-8e2a-39b818928009
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ffb5c6e1457a846bf211dfeb075f3270a7269736
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33263048"
---
# <a name="restorefile-transact-sql"></a>restorefile (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada archivo restaurado, incluidos los restaurados indirectamente por el nombre de grupo de archivos. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Número de identificación único que identifica la operación de restauración correspondiente. Referencias **RestoreHistory (restore_history_id)**.|  
|**file_number**|**numeric(10,0)**|Número de identificación de archivo del archivo restaurado. Este número debe ser único en cada base de datos. Puede ser NULL.<br /><br /> Si una base de datos se revierte a una instantánea de base de datos, este valor se llena del mismo modo que en una restauración completa.|  
|**destination_phys_drive**|**nvarchar(260)**|Unidad o partición en la que se ha restaurado el archivo. Puede ser NULL.<br /><br /> Si una base de datos se revierte a una instantánea de base de datos, este valor se llena del mismo modo que en una restauración completa.|  
|**destination_phys_name**|**nvarchar(260)**|Nombre de archivo, sin la información de unidad o partición, en el que se ha restaurado el archivo. Puede ser NULL.<br /><br /> Si una base de datos se revierte a una instantánea de base de datos, este valor se llena del mismo modo que en una restauración completa.|  
  
## <a name="remarks"></a>Comentarios  
 Para reducir el número de filas en esta tabla y en otras tablas de historial y de copia de seguridad, ejecute el [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restaurar tablas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [restorehistory &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorehistory-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
