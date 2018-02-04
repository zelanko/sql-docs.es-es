---
title: backupmediafamily (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b2435ce3fe98104aaf3bbb857e89779adb221e4
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada familia de medios. Si una familia de medios reside en un conjunto de medios reflejado, la familia tiene una fila independiente para cada reflejo del conjunto de medios. Esta tabla se almacena en la **msdb** base de datos.  
    
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Número de identificación exclusivo que identifica el conjunto de medios al que pertenece esta familia. References **backupmediaset(media_set_id)**|  
|**family_sequence_number**|**tinyint**|Posición de esta familia de medios en el conjunto de medios.|  
|**media_family_id**|**uniqueidentifier**|Número de identificación exclusivo que identifica a la familia de medios. Puede ser NULL.|  
|**media_count**|**int**|Número de medios en la familia. Puede ser NULL.|  
|**logical_device_name**|**nvarchar(128)**|Nombre de este dispositivo de copia de seguridad en **sys.backup_devices.name**. Si se trata de un dispositivo de copia de seguridad temporal (en lugar de un dispositivo de copia de seguridad permanente que existe en **sys.backup_devices**), el valor de **logical_device_name** es NULL.|  
|**physical_device_name**|**nvarchar(260)**|Nombre físico del dispositivo de copia de seguridad. Puede ser NULL.|  
|**device_type**|**tinyint**|Tipo de dispositivo de copia de seguridad:<br /><br /> 2 = Disco<br /><br /> 5 = Cinta<br /><br /> 7 = Dispositivo virtual<br /><br /> 105 = Dispositivo de copia de seguridad permanente<br /><br /> Puede ser NULL.<br /><br /> Todos los nombres de dispositivos permanentes y los números de dispositivo pueden encontrarse en **sys.backup_devices**.|  
|**physical_block_size**|**int**|Tamaño de bloque físico utilizado para escribir en la familia de medios. Puede ser NULL.|  
|**mirror**|**tinyint**|Número de reflejo (0-3)|  
  
## <a name="remarks"></a>Comentarios  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY rellena las columnas de la **backupmediaset** tabla con los valores apropiados del encabezado del conjunto de medios.  
  
 Para reducir el número de filas en esta tabla y en otras tablas de historial y de copia de seguridad, ejecute el [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restauración tablas &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tablas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
