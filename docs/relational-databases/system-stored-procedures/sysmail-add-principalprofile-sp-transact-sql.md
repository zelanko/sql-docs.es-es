---
title: sysmail_add_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0a8db1f3b8d9bc209b6f8ed238cbf0be6177e578
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017819"
---
# <a name="sysmailaddprincipalprofilesp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permiso a un usuario o un rol de base de datos para usar un perfil de Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @principal_id = ] principal_id` El identificador de usuario de base de datos o del rol en el **msdb** base de datos para la asociación. *principal_id* es **int**, su valor predeterminado es null. Cualquier *principal_id* o *principal_name* debe especificarse. Un *principal_id* de **0** convierte este perfil en público, conceder acceso a todas las entidades de la base de datos.  
  
`[ @principal_name = ] 'principal_name'` El nombre de usuario de base de datos o del rol en el **msdb** base de datos para la asociación. *principal_name* es **sysname**, su valor predeterminado es null. Cualquier *principal_id* o *principal_name* debe especificarse. Un *principal_name* de **'public'** convierte este perfil en público, conceder acceso a todas las entidades de la base de datos.  
  
`[ @profile_id = ] profile_id` El identificador del perfil para la asociación. *profile_id* es **int**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* debe especificarse.  
  
`[ @profile_name = ] 'profile_name'` El nombre del perfil para la asociación. *nombre_perfil* es **sysname**, no tiene ningún valor predeterminado. Cualquier *profile_id* o *profile_name* debe especificarse.  
  
`[ @is_default = ] is_default` Especifica si este perfil es el perfil predeterminado para la entidad de seguridad. Una entidad de seguridad debe tener solo un perfil predeterminado. *is_default* es **bit**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Para convertir un perfil público, especifique un **@principal_id** de **0** o un **@principal_name** de **pública**. Un perfil público está disponible para todos los usuarios de la **msdb** de base de datos, aunque los usuarios también deben ser un miembro de **DatabaseMailUserRole** ejecutar **sp_send_dbmail**.  
  
 El usuario de la base de datos solo puede tener un perfil predeterminado. Cuando **@is_default** es '**1**' y el usuario ya está asociado con uno o varios perfiles, el perfil especificado se convierte en el perfil predeterminado para el usuario. El perfil predeterminado anterior sigue estando asociado con el usuario, pero ya no es el perfil predeterminado.  
  
 Cuando **@is_default** es '**0**' y no existe otra asociación, el procedimiento almacenado devuelve un error.  
  
 El procedimiento almacenado **sysmail_add_principalprofile_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Crear una asociación y configurar el perfil predeterminado**  
  
 En el ejemplo siguiente se crea una asociación entre el perfil denominado `AdventureWorks Administrator Profile` y **msdb** usuario de base de datos `ApplicationUser`. El perfil es el predeterminado del usuario.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B. Convertir un perfil en el perfil público predeterminado**  
  
 El ejemplo siguiente configura el perfil `AdventureWorks Public Profile` el perfil público predeterminado para los usuarios de la **msdb** base de datos.  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
