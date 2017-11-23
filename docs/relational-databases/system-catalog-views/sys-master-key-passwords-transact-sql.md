---
title: Sys.master_key_passwords (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs: TSQL
helpviewer_keywords: sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f00190c24d06f888767343270f77dfdeea8ee7b2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysmasterkeypasswords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada contraseña de la clave maestra de base de datos agregada con la **sp_control_dbmasterkey_password** procedimiento almacenado. Las contraseñas que se usan para proteger las claves maestras se almacenan en el almacén de credenciales. El nombre de credencial sigue este formato: ##DBMKEY_<database_family_guid>_<random_password_guid>##. La contraseña se almacena como el secreto de la credencial. Para cada contraseña agregada con **sp_control_dbmasterkey_password**, hay una fila en **sys.credentials**.  
  
 Cada fila de esta vista muestra una **credential_id** y **family_guid** de una base de datos de la clave maestra de la que está protegida por la contraseña asociada con esa credencial. Una combinación con **sys.credentials** en el **credential_id** devolverá campos útiles, como el **create_date** y nombre de la credencial.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|Id. de la credencial a la que pertenece la contraseña. Este identificador es único en la instancia del servidor.|  
|**family_guid**|**uniqueidentifier**|Id. único de la base de datos original cuando se creó. Este GUID sigue igual después de restaurar o adjuntar la base de datos, incluso si se cambia el nombre de la base de datos.<br /><br /> Si se produce un error en el descifrado automático con la clave maestra de servicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la **family_guid** para identificar las credenciales que pueden contener la contraseña utilizada para proteger la clave maestra de base de datos.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
