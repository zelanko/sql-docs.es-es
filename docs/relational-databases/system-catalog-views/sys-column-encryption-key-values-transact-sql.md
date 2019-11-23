---
title: Sys. column_encryption_key_values (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c5dc4f2dc42452560162d214844e2264cd0e5e9
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593804"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>Sys. column_encryption_key_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los valores cifrados de las claves de cifrado de columnas (las CEK) creadas con la clave de cifrado de [creación](../../t-sql/statements/create-column-encryption-key-transact-sql.md) de columna o la instrucción [Transact-SQL &#40;&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) de la clave de cifrado Alter Column. Cada fila representa un valor de CEK, cifrado con una clave maestra de columna (CMK).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|IDENTIFICADOR del CEK en la base de datos.|  
|**column_master_key_id**|**int**|IDENTIFICADOR de la clave maestra de columna que se usó para cifrar el valor de CEK.|  
|**encrypted_value**|**varbinary(8000)**|Valor CEK cifrado con el CMK especificado en column_master_key_id.|  
|**encryption_algorithm_name**|**sysname**|Nombre de un algoritmo utilizado para cifrar el valor de CEK.<br /><br /> Nombre del algoritmo de cifrado usado para cifrar el valor. El algoritmo para los proveedores de sistema debe ser **RSA_OAEP**.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso **ver cualquier clave de cifrado de columna** .  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Información general sobre la administración de claves de Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [Administración de claves para Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
