---
title: sp_delete_backup (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4125fa3a9a3a836b7cc710f58db0563b74eb8357
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdeletebackup-transact-sql"></a>sp_delete_backup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Elimina todas las instantáneas y el archivo de copia de seguridad que componen una copia de seguridad instantánea de la base de datos especificada. Este procedimiento almacenado del sistema es el único método recomendado para administrar conjuntos de copia de seguridad de instantánea. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *[ @backup_url =] backup_meta_file_url*  
 La dirección URL de la copia de seguridad va a eliminar, lo que elimina todas las instantáneas que componen el conjunto incluido el propio archivo de copia de seguridad especificado de la copia de seguridad.  
  
 *[ @db_name =] database_name*  
 El nombre de la base de datos que contiene la instantánea que se va a eliminar. Cuando un nombre de base de datos es siempre, el sistema comprueba que la dirección URL de copia de seguridad proporcionado es una dirección URL de copia de seguridad para la base de datos especificada y usa [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para eliminar cada instantánea. Si no se proporciona ningún nombre de base de datos, no se realiza esta comprobación de base de datos.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY DATABASE o el permiso ALTER en la base de datos especificada.  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
