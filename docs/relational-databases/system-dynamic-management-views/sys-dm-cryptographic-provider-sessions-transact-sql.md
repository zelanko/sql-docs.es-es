---
description: sys.dm_cryptographic_provider_sessions (Transact-SQL)
title: Sys. dm_cryptographic_provider_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cryptographic_provider_sessions
- dm_cryptographic_provider_sessions_TSQL
- sys.dm_cryptographic_provider_sessions_TSQL
- dm_cryptographic_provider_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_sessions dynamic management function
ms.assetid: 9a4de02b-1a07-4850-979a-0861fddb7f9d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 37a8854da08439c4dc3984bcdfc61a8695467c2b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455022"
---
# <a name="sysdm_cryptographic_provider_sessions-transact-sql"></a>sys.dm_cryptographic_provider_sessions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve información acerca de las sesiones abiertas para un proveedor criptográfico.  
 
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.dm_cryptographic_provider_sessions(session_identifier)  
```  
  
## <a name="arguments"></a>Argumentos  
 *session_identifier*  
 Un entero que indica las sesiones que se van a devolver.  
  
 0 = Conexión actual solo  
  
 1 = Todas las conexiones criptográficas  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**provider_id**|**int**|Número de identificación del proveedor de servicios criptográficos.|  
|**session_handle**|**varbytes (8)**|Controlador de la sesión criptográfico.|  
|**identity**|**nvarchar(128)**|Identidad utilizada para autenticar con el proveedor criptográfico.|  
|**spid**|**short**|Id. de la sesión SPID de la conexión. Para más información, vea [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md).|  
  
## <a name="remarks"></a>Observaciones  
 La vista **Sys. dm_cryptographic_provider_sessions** es visible para el público de la conexión actual. Para ver todas las conexiones criptográficas, debe tener el permiso **control** Server.  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
