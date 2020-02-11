---
title: Sys. dm_cryptographic_provider_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_properties_TSQL
- sys.dm_cryptographic_provider_properties
- sys.dm_cryptographic_provider_properties_TSQL
- dm_cryptographic_provider_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_properties dynamic management view
ms.assetid: 024b0095-6766-4189-a39a-d316c5ec2874
author: stevestein
ms.author: sstein
ms.openlocfilehash: cc1e0915fb48b42429bb2821476f98154ac39451
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68005102"
---
# <a name="sysdm_cryptographic_provider_properties-transact-sql"></a>sys.dm_cryptographic_provider_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre los proveedores de servicios criptográficos registrados.  
  
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|Número de identificación del proveedor de servicios criptográficos.|  
|guid|**uniqueidentifier**|Proveedor único GUID.|  
|provider_version|**nvarchar(256)**|Versión del proveedor con el formato '*AA.BB.CCCC.DD*'.|  
|sqlcrypt_version|**nvarchar(256)**|Versión principal de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] API de cifrado con el formato '*AA.BB.CCCC.DD*'.|  
|friendly_name|**nvarchar (2048)**|El proveedor proporcionó el nombre.|  
|authentication_type|**nvarchar(256)**|WINDOWS, BASIC u OTHER.|  
|symmetric_key_support|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|symmetric_key_export|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|symmetric_key_import|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|symmetric_key_persistance|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|asymmetric_key_support|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|asymmetric_key_export|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|symmetric_key_import|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
|symmetric_key_persistance|**tinyint**|0 (no admitido)<br /><br /> 1 (admitido)|  
  
## <a name="remarks"></a>Observaciones  
 La vista sys.dm_cryptographic_provider_properties está visible para la función public.  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [Funciones y vistas de administración dinámica relacionadas con la seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
