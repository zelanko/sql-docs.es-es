---
title: managed_backup. sp_backup_config_advanced (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0178d4df6a5941b8896e6ff530802fd4c6bc6909
ms.sourcegitcommit: 64e96ad1ce6c88c814e3789f0fa6e60185ec479c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2020
ms.locfileid: "77652954"
---
# <a name="managed_backupsp_backup_config_advanced-transact-sql"></a>managed_backup. sp_backup_config_advanced (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura las opciones avanzadas de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 Nombre de la base de datos para habilitar la copia de seguridad administrada en una base de datos específica. Si es NULL o *, esta copia de seguridad administrada se aplica a todas las bases de datos del servidor.  
  
 @encryption_algorithm  
 El nombre del algoritmo de cifrado utilizado durante la copia de seguridad para cifrar el archivo de copia de seguridad. Es @encryption_algorithm de **tipo SYSNAME**. Es un parámetro obligatorio al configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez para la base de datos. Especifique **NO_ENCRYPTION** si no desea cifrar el archivo de copia de seguridad. Al cambiar los [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] valores de configuración, este parámetro es opcional; si no se especifica el parámetro, se conservan los valores de configuración existentes. Los valores permitidos para este parámetro son:  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Para obtener más información sobre algoritmos de cifrado, vea [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
 @encryptor_type  
 El tipo de sistema de cifrado, que puede ser "CERTIFICAte" o "ASYMMETRIC_KEY". Es @encryptor_type de tipo **nvarchar (32)**. Este parámetro es opcional si se especifica NO_ENCRYPTION para el @encryption_algorithm parámetro.  
  
 @encryptor_name  
 Nombre de un certificado existente o clave asimétrica que se usa para cifrar la copia de seguridad. Es @encryptor_name de **tipo SYSNAME**. Si utiliza una clave asimétrica, debe configurarse con la administración de claves extendida (EKM). Este parámetro es opcional si se especifica NO_ENCRYPTION para el @encryption_algorithm parámetro.  
  
 Para obtener más información, vea [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 @local_cache_path  
 Todavía no se admite este parámetro.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol de base de datos **db_backupoperator** , con permisos **ALTER any Credential** y permisos **Execute** en **sp_delete_backuphistory** procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se establecen las opciones [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de configuración avanzadas de para la instancia de SQL Server.  
  
```sql
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [managed_backup. sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup. sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
