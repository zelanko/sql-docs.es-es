---
title: Sys.fn_db_backup_file_snapshots (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/03/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b9d7d2c500173213f893c83d10e0a650d90e9ee
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>Sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve las instantáneas de Azure asociadas a los archivos de base de datos. Si no se encuentra la base de datos especificada o si los archivos de base de datos no se almacenan en el servicio de almacenamiento de blobs de Microsoft Azure, se devuelve ninguna fila. Use esta función del sistema junto con la **sys.sp_delete_backup_file_snapshot** procedimiento para identificar y eliminar huérfanas las instantáneas de copia de seguridad almacenado del sistema. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_name*  
 El nombre de la base de datos que se está consultando. Si es NULL, esta función se ejecuta en el ámbito de base de datos actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|file_id|**int**|El identificador de archivo para la base de datos. No admite valores NULL.|  
|snapshot_time|**nvarchar (260)**|La marca de tiempo de la instantánea porque es devuelto por la API de REST. Devuelve NULL si no existe ninguna instantánea.|  
|snapshot_url|**nvarchar(360)**|La dirección URL completa a la instantánea de archivo. Devuelve un valor NULL si no hay instantáneas existe.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_backup_file_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
