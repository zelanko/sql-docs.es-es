---
title: managed_backup.sp_backup_config_advanced (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c3f19fed072e693de6bbebb53354eae8c0bfaa0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827913"
---
# <a name="managedbackupspbackupconfigadvanced-transact-sql"></a>managed_backup.sp_backup_config_advanced (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura las opciones avanzadas de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 El nombre de la base de datos para habilitar la copia de seguridad administrada en una base de datos específica. Si es NULL o *, a continuación, esta copia de seguridad administrada se aplica a todas las bases de datos en el servidor.  
  
 @encryption_algorithm  
 El nombre del algoritmo de cifrado utilizado durante la copia de seguridad para cifrar el archivo de copia de seguridad. El @encryption_algorithm es **SYSNAME**. Es un parámetro obligatorio al configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez para la base de datos. Especificar **NO_ENCRYPTION** si no desea cifrar el archivo de copia de seguridad. Al cambiar la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], este parámetro es opcional, si se conserva el parámetro y no se especifica, los valores de configuración existentes se conservan. Los valores permitidos para este parámetro son:  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Para obtener más información sobre algoritmos de cifrado, vea [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md).  
  
 @encryptor_type  
 El tipo de sistema de cifrado, que puede ser cualquier certificado' ' o ' ASYMMETRIC_KEY ". El @encryptor_type es **nvarchar (32)**. Este parámetro es opcional si especifica NO_ENCRYPTION para el @encryption_algorithm parámetro.  
  
 @encryptor_name  
 Nombre de un certificado existente o clave asimétrica que se usa para cifrar la copia de seguridad. El @encryptor_name es **SYSNAME**. Si utiliza una clave asimétrica, debe configurarse con la administración de claves extendida (EKM). Este parámetro es opcional si especifica NO_ENCRYPTION para el @encryption_algorithm parámetro.  
  
 Para obtener más información, vea [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 @local_cache_path  
 Este parámetro no se admite todavía.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere la pertenencia a **db_backupoperator** rol, la base de datos con **ALTER ANY CREDENTIAL** permisos, y **EXECUTE** permisos **sp_delete_ backuphistory** procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente establece las opciones de configuración avanzada para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server.  
  
```  
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
