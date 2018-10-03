---
title: Sys.column_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.column_encryption_keys
- column_encryption_keys_TSQL
- sys.column_encryption_keys_TSQL
- column_encryption_keys
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_keys catalog view
ms.assetid: 43980dd8-b9b1-4869-a304-2c183ae8977d
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83dde1e60b9c9dd78a76c4bfa6afa86ac23f1bd7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756023"
---
# <a name="syscolumnencryptionkeys--transact-sql"></a>Sys.column_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-xxx-md.md)]

  Devuelve información acerca de las claves de cifrado de columna (las CEK) creadas con el [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) instrucción. Cada fila representa una CEK.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|El nombre de la CMK.|  
|**column_encryption_key_id**|**int**|Id. de la CEK.|  
|**create_date**|**datetime**|Fecha de que creación de la CEK.|  
|**modify_date**|**datetime**|Fecha de que la CEK se modificó por última vez.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW ANY COLUMN ENCRYPTION KEY** permiso.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
