---
title: sp_enclave_send_keys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6540cdd36cccba4f5a7ccb3beddf31ce00cd9107
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394147"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Envía columna enclave habilitado todas las claves de cifrado en la base de datos al enclave usando [Always Encrypted con enclaves seguros &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintaxis  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argumentos

Este procedimiento almacenado no tiene ningún argumento.

## <a name="return-value"></a>Valor devuelto

Este procedimiento almacenado no tiene ningún valor devuelto.
  
## <a name="result-sets"></a>Conjuntos de resultados

Este procedimiento almacenado no tiene ningún conjunto de resultados.
  
## <a name="remarks"></a>Comentarios

**sp_enclave_send_keys** envía las claves de cifrado de columna enclave habilitada para el enclave si se cumplen las condiciones siguientes:

- El enclave está habilitado en la instancia de SQL Server.
- **sp_enclave_send_keys** se ha invocado desde una aplicación mediante un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador cliente, compatibilidad con Always Encrypted con enclaves seguros mediante una conexión de base de datos que tiene cálculos de Always Encrypted y de enclave habilitados.

## <a name="permissions"></a>Permisos

 Requerir la **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** y **VIEW ANY COLUMN MASTER KEY DEFINITION** permisos en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Vea también

 [Always Encrypted con enclaves seguros &#40;motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Tutorial: Creación y uso de índices en columnas basadas en enclave mediante el cifrado aleatorio](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [Invocar las operaciones de indización mediante claves de cifrado de columna almacenada en caché](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [Índices en columnas Enclave habilitados mediante el cifrado aleatorio](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [Consideraciones para la migración de base de datos y AlwaysOn](../security/encryption/always-encrypted-enclaves.md#considerations-for-alwayson-and-database-migration)
