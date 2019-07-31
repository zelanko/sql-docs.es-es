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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ced2feee2227ba1db492f721f57907069c5d99
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661358"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Envía todas las claves de cifrado de columna habilitadas para enclave en la base de datos a la enclave usada por [Always Encrypted con el motor de base de datos &#40;&#41;de enclaves seguro](../../relational-databases/security/encryption/always-encrypted-enclaves.md).

## <a name="syntax"></a>Sintaxis  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>Argumentos

Este procedimiento almacenado no tiene argumentos.

## <a name="return-value"></a>Valor devuelto

Este procedimiento almacenado no tiene ningún valor devuelto.
  
## <a name="result-sets"></a>Conjuntos de resultados

Este procedimiento almacenado no tiene ningún conjunto de resultados.
  
## <a name="remarks"></a>Comentarios

**sp_enclave_send_keys** envía claves de cifrado de columnas habilitadas para enclave a enclave si se cumplen todas las condiciones siguientes:

- Enclave está habilitado en la instancia de SQL Server.
- **sp_enclave_send_keys** se ha invocado desde una aplicación que usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un controlador cliente, lo que admite la Always Encrypted con enclaves seguro mediante una conexión de base de datos que tenga habilitados los cálculos de Always Encrypted y enclave.

## <a name="permissions"></a>Permisos

 Requiere la **definición de clave de cifrado ver cualquier columna** y ver los permisos de **definición de clave maestra de columna** en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>Vea también

 [Always Encrypted con enclaves &#40;seguros motor de base de datos&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Tutorial: Crear y usar índices en columnas habilitadas para enclave mediante el cifrado aleatorio](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [Invocar operaciones de indexación mediante claves de cifrado de columnas almacenadas en caché](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [Índices en columnas habilitadas para enclave mediante el cifrado aleatorio](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [Consideraciones sobre AlwaysOn y la migración de bases de datos](../security/encryption/always-encrypted-enclaves.md#anchorname-1-considerations-availability-groups-db-migration)
