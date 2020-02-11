---
title: sp_delete_backup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 49eb0906a9a5af1fec2abfeec3ef58845b605e69
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67941822"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Elimina todas las instantáneas y el archivo de copia de seguridad que componen un conjunto de copia de seguridad de instantáneas de la base de datos especificada. Este procedimiento almacenado del sistema es el único método recomendado para administrar conjuntos de copia de seguridad de instantáneas. Para obtener más información, vea [Copias de seguridad de instantáneas de archivo para archivos de base de datos en Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *[ @backup_url =] backup_meta_file_url*  
 Dirección URL de la copia de seguridad que se va a eliminar, que elimina todas las instantáneas que componen el conjunto de copia de seguridad especificado, incluido el propio archivo de copia de seguridad.  
  
 *[ @db_name =] database_name*  
 Nombre de la base de datos que contiene la instantánea que se va a eliminar. Cuando se proporciona un nombre de base de datos, el sistema comprueba si la dirección URL de copia de seguridad proporcionada es una dirección URL de copia de seguridad para la base de datos especificada y usa [sp_delete_backup_file_snapshot &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para eliminar cada instantánea. Si no se proporciona ningún nombre de base de datos, no se realiza esta comprobación de base de datos.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY DATABASE o el permiso ALTER en la base de datos especificada.  
  
## <a name="see-also"></a>Consulte también  
 [Sys. fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
