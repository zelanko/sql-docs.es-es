---
title: sp_delete_backup_file_snapshot (Transact-SQL) | Documentos de Microsoft
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8d0a71b2275010490f61d433975cd6c3fffbe9b1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletebackupfilesnapshot-transact-sql"></a>sp_delete_backup_file_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Elimina una instantánea de copia de seguridad especificada de la base de datos especificada. Utilice este sistema de procedimiento almacenado junto con el **sys.fn_db_backup_file_snapshots** huérfanos de función del sistema para identificar y eliminar las instantáneas de copia de seguridad. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N’<database_name>  
    , [ @snapshot_url = ] N’<snapshot_url>  
```  
  
## <a name="arguments"></a>Argumentos  
 *[ @db_name =] database_name*  
 El nombre de la base de datos que contiene la instantánea que se va a eliminar, proporcionado como una cadena Unicode.  
  
 *[ @snapshot_url =] snapshot_url*  
 La dirección URL de la instantánea se elimina, se proporciona como una cadena Unicode.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY DATABASE.  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
