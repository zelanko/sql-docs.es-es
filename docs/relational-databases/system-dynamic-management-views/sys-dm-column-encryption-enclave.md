---
title: Sys. dm_column_encryption_enclave (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d10bef0df04501c177086b6c89b3f67dec3bab10
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73599248"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-SQL)
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Devuelve los contadores de rendimiento para el enclave seguro para Always Encrypted. Para más información, consulte [Always Encrypted con enclaves seguros](../security/encryption/always-encrypted-enclaves.md).

Si el enclave está configurado y se ha inicializado correctamente después del último reinicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de, la vista contiene exactamente una fila. Si el enclave no está configurado o no se ha inicializado correctamente, la vista no devuelve ninguna fila. 

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|Número actual de sesiones de cliente que usan enclave.|  
|current_column_encryption_key_count|**int**|Recuento de claves de cifrado de columna que el enclave contiene actualmente.|  
|current_memory_size_kb|**bigint**|Tamaño de memoria de enclave en KB|  
|total_evicted_session_count|**bigint**|Número total de sesiones de enclave expulsadas desde el último reinicio del servidor.|   
  
## <a name="permissions"></a>Permisos  
Requiere el permiso `VIEW SERVER STATE`.   
  
## <a name="examples"></a>Ejemplos  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Configuración del tipo de enclave como opción de configuración del servidor Always Encrypted](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
