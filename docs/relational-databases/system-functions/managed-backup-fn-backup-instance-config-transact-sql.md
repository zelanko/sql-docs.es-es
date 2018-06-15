---
title: managed_backup.fn_backup_instance_config (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4dae80911e6508a1a398cf208300bf4145faeecc
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33230000"
---
# <a name="managedbackupfnbackupinstanceconfig-transact-sql"></a>managed_backup.fn_backup_instance_config (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila con la configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server.  
  
 Utilice este procedimiento almacenado para revisar o para determinar la configuración predeterminada actual de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia de SQL Server.  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="Arguments"></a> Argumentos  
 None  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|Muestra 1 cuando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada y 0 cuando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está deshabilitada.|  
|credential_name|SYSNAME|La Credencial SQL predeterminada que se usa para autenticarse en el almacenamiento.|  
|retention_days|INT|Período de retención predeterminado establecido en el nivel de instancia.|  
|storage_url|NVARCHAR (1024)|La dirección URL de la cuenta de almacenamiento predeterminada establecida en el nivel de instancia.|  
|encryption_algorithm|SYSNAME|Nombre del algoritmo de cifrado. Se establece en NULL si no se especifica el cifrado.|  
|encryptor_type|NVARCHAR (32)|Tipo de sistema de cifrado usado: certificado o clave asimétrica. Se establece en NULL si no hay ningún sistema de cifrado especificado.|  
|encryptor_name|SYSNAME|Nombre del certificado o de la clave asimétrica. Se establece en NULL si no hay ningún nombre especificado|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Debe pertenecer a la **db_backupoperator** rol de base de datos con **ALTER ANY CREDENTIAL** permisos. El usuario no se debe denegar **VIEW ANY DEFINITION** permisos.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia en la que se ejecuta:  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
