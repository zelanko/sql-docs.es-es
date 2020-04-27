---
title: Sys. fn_db_backup_file_snapshots (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5159b72cb91cfdcf21129c6216cab4cf0e8d4dea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "68120271"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>Sys. fn_db_backup_file_snapshots (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve instantáneas de Azure asociadas a los archivos de base de datos. Si no se encuentra la base de datos especificada o si los archivos de base de datos no están almacenados en el servicio Microsoft Azure BLOB Storage, no se devuelve ninguna fila. Utilice esta función del sistema junto con el procedimiento almacenado del sistema **Sys. sp_delete_backup_file_snapshot** para identificar y eliminar las instantáneas de copia de seguridad huérfanas. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Database_name*  
 Nombre de la base de datos que se consulta. Si es NULL, esta función se ejecuta en el ámbito de la base de datos actual.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|file_id|**int**|IDENTIFICADOR de archivo de la base de datos. No admite valores NULL.|  
|snapshot_time|**nvarchar(260)**|Marca de tiempo de la instantánea tal como la devuelve la API de REST. Devuelve NULL si no existe ninguna instantánea.|  
|snapshot_url|**nvarchar(360)**|Dirección URL completa de la instantánea del archivo. Devuelve NULL si no existe ninguna instantánea.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="see-also"></a>Consulte también  
 [sp_delete_backup_file_snapshot &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
