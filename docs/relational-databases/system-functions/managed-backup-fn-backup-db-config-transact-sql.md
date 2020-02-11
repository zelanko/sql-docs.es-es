---
title: managed_backup. fn_backup_db_config (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_backup_db_config
- smart_admin.fn_backup_db_config_TSQL
- fn_backup_db_config
- fn_backup_db_config_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_db_config
- fn_backup_db_config
ms.assetid: 7c755d8a-64dd-44b2-be5e-735d30758900
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a23f8eb64ae99b999cdf6b16f1c888383a88c147
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067777"
---
# <a name="managed_backupfn_backup_db_config-transact-sql"></a>managed_backup. fn_backup_db_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve 0, 1 o más filas con la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Devuelve una fila para la base de datos especificada o la información de todas las bases de datos configuradas con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de la instancia.  
  
 Utilice este procedimiento almacenado para revisar o para determinar la configuración actual de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos o para todas las bases de datos de una instancia de SQL Server.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.fn_backup_db_config ('database_name' | '' | NULL)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @db_name  
 El nombre de la base de datos. El @db_name parámetro es de **tipo SYSNAME**. Si una cadena vacía o un valor NULL se pasan a este parámetro, se devuelve la información sobre todas las bases de datos de la instancia de SQL Server.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|db_name|SYSNAME|nombre de base de datos.|  
|db_guid|UNIQUEIDENTIFIER|Identificador que identifica la base de datos de forma única.|  
|is_availability_database|BIT|Si la base de datos participa en un grupo de disponibilidad. El valor 1 indica que la base de datos es una base de datos de disponibilidad y el valor 0, que no lo es.|  
|is_dropped|BIT|El valor 1 indica que se trata de una base de datos quitada.|  
|credential_name|SYSNAME|Nombre de la credencial SQL que se usa para autenticarse en la cuenta de almacenamiento. El valor NULL indica que no se ha establecido ninguna credencial de SQL.|  
|retention_days|INT|Período de retención actual, en días. El valor NULL indica que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] nunca se configuró para esta base de datos.|  
|is_managed_backup_enabled|INT|Indica si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada actualmente para esta base de datos. El valor 1 indica que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada y el valor 0 indica que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está deshabilitada para esta base de datos.|  
|storage_url|NVARCHAR (1024)|Dirección URL de la cuenta de almacenamiento.|  
|Encryption_algorithm|NCHAR (20)|Devuelve el algoritmo de cifrado actual que usar cuando se cifra la copia de seguridad.|  
|Encryptor_type|NCHAR(15)|Devuelve el valor del sistema de cifrado: certificado o clave asimétrica.|  
|Encryptor_name|NCHAR(long_max_de_cert/nombre_clave_asim)|Nombre del certificado o de la clave asimétrica.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol de base de datos **db_backupoperator** con permisos **ALTER any Credential** . No se debe denegar el permiso **View any Definition** a los usuarios.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] devuelve la configuración para ' TestDB '  
  
 Para cada fragmento de código, seleccione 'tsql' en el campo de atributo language.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config('TestDB')  
```  
  
 El ejemplo siguiente devuelve la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para todas las bases de datos de la instancia de SQL Server en la que se ejecuta.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL)  
```  
  
  
