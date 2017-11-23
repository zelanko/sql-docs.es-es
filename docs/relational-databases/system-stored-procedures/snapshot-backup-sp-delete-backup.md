---
title: sp_delete_backup (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/03/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 185e0a7eca792b25413145ffcabedf5441deb34b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="snapshot-backup---spdeletebackup"></a>Copia de seguridad de instantánea: sp_delete_backup
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Elimina todas las instantáneas y el archivo de copia de seguridad que componen una copia de seguridad instantánea de la base de datos especificada. Este procedimiento almacenado del sistema es el único método recomendado para administrar conjuntos de copia de seguridad de instantánea. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
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
 El nombre de la base de datos que contiene la instantánea que se va a eliminar. Cuando se proporciona un nombre de base de datos, el sistema comprueba que la dirección de URL de copia de seguridad proporcionada es una dirección URL de copia de seguridad para la base de datos especificada y usa [sp_delete_backup_file_snapshot &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) para eliminar cada instantánea. Si no se proporciona ningún nombre de base de datos, no se realiza esta comprobación de base de datos.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY DATABASE o el permiso ALTER en la base de datos especificada.  
  
## <a name="see-also"></a>Vea también  
 [Sys.fn_db_backup_file_snapshots &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
