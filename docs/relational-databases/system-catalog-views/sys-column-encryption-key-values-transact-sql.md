---
title: Sys.column_encryption_key_values (Transact-SQL) | Documentos de Microsoft
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
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: e89df0a5d451ce280bb884e49f29c189f89d6e1a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39561555"
---
# <a name="syscolumnencryptionkeyvalues-transact-sql"></a>Sys.column_encryption_key_values (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los valores cifrados de la columna de claves de cifrado (las CEK) creadas con una la [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) o [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)instrucción. Cada fila representa un valor de una CEK, cifrado con una clave maestra de columna (CMK).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|Id. de la CEK en la base de datos.|  
|**column_master_key_id**|**int**|Id. de la clave maestra de columna que se usó para cifrar el valor CEK.|  
|**encrypted_value**|**varbinary(8000)**|Valor de la clave cifrada con la CMK especificada en column_master_key_id.|  
|**encryption_algorithm_name**|**sysname**|Nombre del algoritmo utilizado para cifrar el valor CEK.<br /><br /> Nombre del algoritmo de cifrado usado para cifrar el valor. El algoritmo para los proveedores del sistema debe ser **RSA_OAEP**.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW ANY COLUMN ENCRYPTION KEY** permiso.  
  
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
 [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
