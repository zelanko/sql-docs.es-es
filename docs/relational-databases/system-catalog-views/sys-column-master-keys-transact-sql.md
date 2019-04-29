---
title: sys.column_master_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1cb1740bdb0ae26d91e2a9ad9e2becb69d3b2810
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63013713"
---
# <a name="syscolumnmasterkeys-transact-sql"></a>sys.column_master_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada clave maestra de base de datos agregado mediante el [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) instrucción. Cada fila representa una clave maestra de columna (CMK).  
    
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|El nombre de la CMK.|  
|**column_master_key_id**|**int**|Id. de la clave maestra de columna.|  
|**create_date**|**datetime**|Fecha de que creación de la clave maestra de columna.|  
|**modify_date**|**datetime**|Fecha en la que se modificó por última vez la clave maestra de columna.|  
|**key_store_provider_name**|**sysname**|Nombre del proveedor para el almacén de claves maestras de columna que contiene la CMK. Los valores permitidos son:<br /><br /> MSSQL_CERTIFICATE_STORE - si el almacén de claves maestras de columna es un certificado de Store.<br /><br /> Un valor definido por el usuario, si el almacén de claves maestras de columna es de un tipo personalizado.|  
|**key_path**|**nvarchar(4000)**|Una columna de clave principal específico del almacén ruta de acceso de la clave. El formato de la ruta de acceso depende el tipo de almacén de clave maestra de columna. Ejemplo:<br /><br /> `'CurrentUser/Personal/'<thumbprint>`<br /><br /> Para un almacén de claves maestras de columna personalizada, el desarrollador es responsable de definir lo que una ruta de acceso de clave es para el almacén de claves maestras de columna personalizada.|  
|**allow_enclave_computations**|**bit**|Indica si la clave maestra de columna está enclave habilitado (si las claves de cifrado de columna, cifradas con esta clave maestra, pueden usarse para realizar cálculos dentro de los enclaves seguros del servidor). Para más información, consulte [Always Encrypted con enclaves seguros](../../relational-databases/security/encryption/always-encrypted-enclaves.md).|  
|**signature**|**varbinary(max)**|Una firma digital de **key_path** y **allow_enclave_computations**, usando la clave maestra de columna, al que hace referencia **key_path**.|


  
## <a name="permissions"></a>Permisos  
 Requiere el **VIEW ANY COLUMN MASTER KEY** permiso.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Always Encrypted &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)  
  
  
