---
title: managed_backup. sp_backup_config_basic (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_basic_TSQL
- sp_backup_config_basic
- managed_backup.sp_backup_config_basic
- managed_backup.sp_backup_config_basic_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- managed_backup.sp_backup_config_basic
- sp_backup_config_basic
ms.assetid: 3ad73051-ae9a-4e41-a889-166146e5508f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 684a538030aae91cd50125c82d4a5aee401764eb
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830391"
---
# <a name="managed_backupsp_backup_config_basic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura los [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] valores básicos para una base de datos concreta o para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se puede llamar a este procedimiento por su cuenta para crear una configuración básica de copia de seguridad administrada. Sin embargo, si tiene previsto agregar características avanzadas o una programación personalizada, configure primero esos valores con [managed_backup. sp_backup_config_advanced &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) y [managed_backup. sp_backup_config_schedule &#40;Transact-SQL](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)&#41;antes de habilitar la copia de seguridad administrada con este procedimiento.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 @enable_backup  
 Habilite o deshabilite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la base de datos especificada. @enable_backupEs de **bit**. Parámetro necesario al configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la primera instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si va a cambiar una [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuración existente, este parámetro es opcional. En ese caso, los valores de configuración no especificados conservan sus valores existentes.  
  
 @database_name  
 Nombre de la base de datos para habilitar la copia de seguridad administrada en una base de datos específica.  
  
 @container_url  
 Una dirección URL que indica la ubicación de la copia de seguridad. Cuando @credential_name es null, esta dirección URL es una dirección URL de firma de acceso compartido (SAS) para un contenedor de blobs en Azure Storage y las copias de seguridad usan la nueva funcionalidad de copia de seguridad para bloquear BLOB. Para obtener más información, consulte [Descripción de SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Cuando @credential_name se especifica, se trata de una dirección URL de cuenta de almacenamiento y las copias de seguridad usan la funcionalidad de BLOB de copia de seguridad en página en desuso.  
  
> [!NOTE]  
>  En este momento solo se admite una dirección URL de SAS para este parámetro.  
  
 @retention_days  
 El período de retención en días de los archivos de copia de seguridad. @storage_urlEs de tipo int. Este es un parámetro obligatorio al configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al cambiar la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuración, este parámetro es opcional. Si no se especifica, los valores de configuración existentes se conservan.  
  
 @credential_name  
 El nombre de la credencial SQL que se usa para autenticar en la cuenta de almacenamiento de Azure. @credentail_namees de **tipo SYSNAME**. Cuando se especifica, la copia de seguridad se almacena en un BLOB en páginas. Si este parámetro es NULL, la copia de seguridad se almacenará como un BLOB en bloques. El BLOB de copia de seguridad en página está en desuso, por lo que es preferible usar la nueva funcionalidad de copia de seguridad de blobs en bloques. Cuando se utiliza para cambiar la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], este parámetro es opcional. Si no se especifica, se conservan los valores de configuración existentes.  
  
> [!WARNING]
>  En este momento no se admite el parámetro ** \@ credential_name** . Solo se admite la copia de seguridad en blobs en bloques, lo que requiere que este parámetro sea NULL.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol de base de datos **db_backupoperator** , con permisos **ALTER any Credential** y permisos **Execute** en **sp_delete_backuphistory** procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 Puede crear el contenedor de la cuenta de almacenamiento y la dirección URL de SAS mediante los comandos Azure PowerShell más recientes. En el ejemplo siguiente se crea un nuevo contenedor, alcontainer, en la cuenta de almacenamiento mystorageaccount y, a continuación, se obtiene una dirección URL de SAS con permisos completos.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 En el ejemplo siguiente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se habilita para la instancia de SQL Server en la que se ejecuta, se establece la Directiva de retención en 30 días, se establece el destino en un contenedor denominado ' ' en una cuenta de almacenamiento denominada ' mystorageaccount '.  
  
```Transact-SQL 
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=1  
                ,@container_url = 'https://mystorageaccount.blob.core.windows.net/mycontainer'  
                ,@retention_days=30;   
GO  
  
```
  
 El ejemplo siguiente deshabilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server en la que se ejecuta.  
  
```Transact-SQL  
Use msdb;  
Go  
EXEC managed_backup.sp_backup_config_basic  
                @enable_backup=0;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [managed_backup. sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
