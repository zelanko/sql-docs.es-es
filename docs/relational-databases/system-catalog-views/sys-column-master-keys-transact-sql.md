---
title: Sys. column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b7c219b2eb56fc299857a5a189ddd9db041f2f47
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73594523"
---
# <a name="syscolumn_master_keys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada clave maestra de base de datos agregada mediante la instrucción [Create Master Key](../../t-sql/statements/create-column-master-key-transact-sql.md) . Cada fila representa una única clave maestra de columna (CMK).  
    
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del CMK.|  
|**column_master_key_id**|**int**|IDENTIFICADOR de la clave maestra de columna.|  
|**create_date**|**datetime**|Fecha en que se creó la clave maestra de columna.|  
|**modify_date**|**datetime**|Fecha en que se modificó por última vez la clave maestra de columna.|  
|**key_store_provider_name**|**sysname**|Nombre del proveedor del almacén de claves maestras de columna que contiene CMK. Los valores permitidos son:<br /><br /> MSSQL_CERTIFICATE_STORE: Si el almacén de claves maestras de columna es un almacén de certificados.<br /><br /> Un valor definido por el usuario, si el almacén de claves maestras de columna es de un tipo personalizado.|  
|**key_path**|**nvarchar(4000)**|Una ruta de acceso específica del almacén de claves maestras de columna de la clave. El formato de la ruta de acceso depende del tipo de almacén de claves maestras de columna. Ejemplo:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Para un almacén de claves maestras de columna personalizado, el desarrollador es responsable de definir qué es una ruta de acceso de clave para el almacén de claves maestras de columna personalizado.|  
|**allow_enclave_computations**|**bit**|Indica si la clave maestra de columna está habilitada para enclave, (si las claves de cifrado de columna, cifradas con esta clave maestra, se pueden usar para los cálculos dentro de enclaves seguras del lado servidor). Para más información, consulte [Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).|  
|**firma**|**varbinary(max)**|Firma digital de **key_path** y **allow_enclave_computations**, generada mediante la clave maestra de columna a la que hace referencia **key_path**.|


  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **ver cualquier clave maestra de columna** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [CREAR clave maestra de columna &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Información general sobre la administración de claves para Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Administración de claves para Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
 
  
  
