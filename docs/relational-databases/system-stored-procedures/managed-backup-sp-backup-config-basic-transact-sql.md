---
title: managed_backup.sp_backup_config_basic (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/03/2016
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
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9a84640449375852f4a618afb1c1282401e784be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="managedbackupspbackupconfigbasic-transact-sql"></a>managed_backup.sp_backup_config_basic (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Configura el [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuración básica para una base de datos específica o para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Este procedimiento puede llamarse en su propio para crear una configuración básica de copia de seguridad administrada. Sin embargo, si planea agregar características avanzadas o una programación personalizada, primero configure las opciones mediante [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md) y [managed_backup.sp_ backup_config_schedule &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md) antes de habilitar la copia de seguridad administrada con este procedimiento.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```Transact-SQL   
EXEC managed_backup.sp_backup_config_basic  
    [@enable_backup = ] { 0 | 1}    ,[@database_name = ] 'database_name'    ,[@container_url = ] 'Azure_Storage_blob_container  
    ,[@retention_days = ] 'retention_period_in_days'    ,[@credential_name = ] 'sql_credential_name'  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @enable_backup  
 Habilite o deshabilite [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la base de datos especificada. El @enable_backup es **bits**. Parámetro obligatorio al configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la primera instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si va a modificar una existente [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuración, este parámetro es opcional. En ese caso, los valores de configuración no se especifica conservan sus valores existentes.  
  
 @database_name  
 El nombre de la base de datos para habilitar la copia de seguridad administrada en una base de datos.  
  
 @container_url  
 Una dirección URL que indica la ubicación de la copia de seguridad. Cuando @credential_name es NULL, esta dirección URL es una dirección URL de firma (SAS) de acceso compartido a un contenedor de blobs en almacenamiento de Azure y las copias de seguridad utilizan la nueva copia de seguridad a la funcionalidad de blob de bloque. Para obtener más información, consulte [descripción SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/). Cuando @credential_name se especifica, se trata de una URL de la cuenta de almacenamiento y las copias de seguridad utilizan la copia de seguridad en desuso a la funcionalidad de blob de página.  
  
> [!NOTE]  
>  Sólo una dirección URL de SAS se admite para este parámetro en este momento.  
  
 @retention_days  
 El período de retención en días de los archivos de copia de seguridad. El @storage_url es INT. Esto es un parámetro obligatorio al configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al cambiar la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuración, este parámetro es opcional. Si no se especifica, los valores de configuración existentes se conservan.  
  
 @credential_name  
 Nombre de la credencial SQL que se usa para autenticarse en la cuenta de almacenamiento de Windows Azure. @credentail_name es **SYSNAME**. Cuando se especifica, la copia de seguridad se almacena en un blob en páginas. Si este parámetro es NULL, la copia de seguridad se almacenará como un blob en bloques. Copia de seguridad en el blob de página está en desuso, por lo que es preferible usar la nueva funcionalidad de copia de seguridad de blob de bloque. Cuando se utiliza para cambiar la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)], este parámetro es opcional. Si no se especifica, se conservan los valores de configuración existentes.  
  
> [!WARNING]  
>  El **@credential_name** parámetro no se admite en este momento. Se admite solo copia de seguridad para bloquear el blob, lo que requiere este parámetro para que sea NULL.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere la pertenencia a **db_backupoperator** rol, la base de datos con **ALTER ANY CREDENTIAL** permisos, y **EXECUTE** permisos **sp_delete_ backuphistory** procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 Puede crear el contenedor de la cuenta de almacenamiento y la dirección URL de SAS mediante los comandos de PowerShell de Azure más recientes. En el ejemplo siguiente se crea un nuevo contenedor, mycontainer, en la cuenta de almacenamiento de mystorageaccount y, a continuación, obtiene una dirección URL de SAS para el mismo con todos los permisos.  
  
```powershell  
$context = New-AzureStorageContext -StorageAccountName mystorageaccount -StorageAccountKey (Get-AzureStorageKey -StorageAccountName mystorageaccount).Primary  
New-AzureStorageContainer -Name mycontainer -Context $context  
New-AzureStorageContainerSASToken -Name mycontainer -Permission rwdl -FullUri -Context $context  
```  
  
 En el ejemplo siguiente se habilita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server que se ejecuta, Establece la directiva de retención en 30 días, Establece el destino en un contenedor denominado 'mycontainer' en una cuenta de almacenamiento denominada 'mystorageaccount'.  
  
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
  
## <a name="see-also"></a>Vea también  
 [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
