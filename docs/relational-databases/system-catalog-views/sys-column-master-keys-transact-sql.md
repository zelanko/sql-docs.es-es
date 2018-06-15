---
title: Sys.column_master_keys (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_master_key_definitions_TSQL
- column_master_key_definitions
- sys.column_master_key_definitions_TSQL
- sys.column_master_key_definitions
- column_master_keys_TSQL
- column_master_keys
- sys.column_master_keys_TSQL
- sys.column_master_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_key_definitions catalog view
- sys.column_master_keys catalog view
ms.assetid: fbec2efa-5fe9-4121-9b34-60497b0b2aca
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7f961586da2bb4bd9a3169fe955d989557535ba7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33181781"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada clave maestra de base de datos agregado mediante la [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) instrucción. Cada fila representa una clave maestra de columna (CMK).  
    
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|El nombre de la CMK.|  
|**column_master_key_id**|**int**|Id. de la clave maestra de columna.|  
|**create_date**|**datetime**|Fecha en que se creó la clave maestra de columna.|  
|**modify_date**|**datetime**|Fecha en la que se modificó por última vez la clave maestra de columna.|  
|**key_store_provider_name**|**sysname**|Nombre del proveedor para el almacén de claves maestras de columna que contiene la CMK. Los valores permitidos son:<br /><br /> MSSQL_CERTIFICATE_STORE: si el almacén de claves maestras de columna es un almacén de certificados.<br /><br /> Un valor definido por el usuario, si el almacén de claves maestras de columna es de un tipo personalizado.|  
|**key_path**|**nvarchar(4000)**|Una columna de clave principal específico del almacén ruta de acceso de la clave. El formato de la ruta de acceso depende del tipo de almacén de clave maestra de columna. Ejemplo:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Para un almacén de claves maestras de columna personalizada, el programador es responsable de definir qué una ruta de acceso de clave es para el almacén de claves maestras de columna personalizado.|  
  
## <a name="permissions"></a>Permissions  
 Requiere la **VIEW ANY COLUMN MASTER KEY** permiso.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
