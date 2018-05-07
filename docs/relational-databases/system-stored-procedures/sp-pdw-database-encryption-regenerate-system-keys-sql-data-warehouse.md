---
title: sp_pdw_database_encryption_regenerate_system_keys (almacenamiento de datos de SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: bb13e323-a984-4462-8b6d-6019c38ddd9d
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ae2da032a42654f39a5b0937393946d71ff1efe8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sppdwdatabaseencryptionregeneratesystemkeys-sql-data-warehouse"></a>sp_pdw_database_encryption_regenerate_system_keys (almacenamiento de datos de SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_database_encryption_regenerate_system_keys** rotar la clave de cifrado del certificado y la base de datos para bases de datos internas que se cifran cuando TDE está habilitado en el dispositivo. incluidos `tempdb`. Esto se realizará correctamente sólo si TDE está habilitado.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption_regenerate_system_keys  ;  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 El procedimiento no tiene parámetros.  
  
 Este procedimiento debe usarse cuando el tráfico en el dispositivo es bajo.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** función fija de base de datos, o **CONTROL SERVER** permiso.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se vuelve a generar las claves de cifrado de base de datos.  
  
```sql  
EXEC sys.sp_pdw_database_encryption_regenerate_system_keys;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_pdw_database_encryption &#40;almacenamiento de datos SQL&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;almacenamiento de datos SQL&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
