---
title: Sys.fn_db_backup_file_snapshots (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
caps.latest.revision: 10
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085bf32115bfe84b00471de27e1fd9c11b3a1ab9
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2018
ms.locfileid: "33231354"
---
# <a name="sysfndbbackupfilesnapshots-transact-sql"></a>Sys.fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve las instantáneas de Azure asociadas a los archivos de base de datos. Si no se encuentra la base de datos especificada o si los archivos de base de datos no se almacenan en el servicio de almacenamiento de blobs de Microsoft Azure, se devuelve ninguna fila. Use esta función del sistema junto con la **sys.sp_delete_backup_file_snapshot** procedimiento para identificar y eliminar huérfanas las instantáneas de copia de seguridad almacenado del sistema. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 El nombre de la base de datos que se está consultando. Si es NULL, esta función se ejecuta en el ámbito de base de datos actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|file_id|**int**|El identificador de archivo para la base de datos. No admite valores NULL.|  
|snapshot_time|**nvarchar(260)**|La marca de tiempo de la instantánea porque es devuelto por la API de REST. Devuelve NULL si no existe ninguna instantánea.|  
|snapshot_url|**nvarchar(360)**|La dirección URL completa a la instantánea de archivo. Devuelve un valor NULL si no hay instantáneas existe.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
