---
title: Sys. master_key_passwords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.master_key_passwords_TSQL
- master_key_passwords_TSQL
- sys.master_key_passwords
- master_key_passwords
dev_langs:
- TSQL
helpviewer_keywords:
- sys.master_key_passwords catalog view
ms.assetid: b8e18cff-a9e6-4386-98ce-1cd855506e03
author: stevestein
ms.author: sstein
ms.openlocfilehash: 926acd9beb00102e19dbc2844e282d74bc890915
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "80752901"
---
# <a name="sysmaster_key_passwords-transact-sql"></a>sys.master_key_passwords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Devuelve una fila por cada contraseña de clave maestra de base de datos agregada mediante el **sp_control_dbmasterkey_password** procedimiento almacenado. Las contraseñas que se usan para proteger las claves maestras se almacenan en el almacén de credenciales. El nombre de la credencial sigue este formato: # #DBMKEY_<database_family_guid>_<random_password_guid> # #. La contraseña se almacena como el secreto de la credencial. Para cada contraseña que se agrega mediante **sp_control_dbmasterkey_password**, hay una fila en **Sys. Credentials**.  
  
 Cada fila de esta vista muestra un **credential_id** y el **family_guid** de una base de datos cuya clave maestra está protegida por la contraseña asociada a esa credencial. Una combinación con **Sys. Credentials** en el **credential_id** devolverá campos útiles, como el **create_date** y el nombre de la credencial.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**credential_id**|**int**|Id. de la credencial a la que pertenece la contraseña. Este identificador es único en la instancia del servidor.|  
|**family_guid**|**uniqueidentifier**|Id. único de la base de datos original cuando se creó. Este GUID sigue igual después de restaurar o adjuntar la base de datos, incluso si se cambia el nombre de la base de datos.<br /><br /> Si se produce un error al descifrar automáticamente la clave [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] maestra de servicio, utiliza el **family_guid** para identificar las credenciales que pueden contener la contraseña usada para proteger la clave maestra de la base de datos.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sp_control_dbmasterkey_password &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [CREAR clave simétrica &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
