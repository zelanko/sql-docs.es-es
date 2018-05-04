---
title: sysmail_update_principalprofile_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5126e0623c540e576f26361c8feee7587367d15
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailupdateprincipalprofilesp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza la información para una asociación entre una entidad de seguridad y un perfil.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@principal_id** =] *principal_id*  
 El identificador del usuario de base de datos o del rol en el **msdb** base de datos de asociación que se va a cambiar. *principal_id* es **int**, su valor predeterminado es null. Cualquier *principal_id* o *principal_name* debe especificarse.  
  
 [ **@principal_name** =] **'***principal_name***'**  
 El nombre del usuario de base de datos o del rol en el **msdb** base de datos de asociación que se va a actualizar. *principal_name* es **sysname**, su valor predeterminado es null. Cualquier *principal_id* o *principal_name* se puede especificar.  
  
 [ **@profile_id** =] *profile_id*  
 Identificador del perfil para la asociación que se va a cambiar. *profile_id* es **int**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* debe especificarse.  
  
 [ **@profile_name** =] **'***profile_name***'**  
 Nombre del perfil para la asociación que se va a cambiar. *profile_name* es **sysname**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* debe especificarse.  
  
 [ **@is_default** =] **'***is_default***'**  
 Determina si este perfil es el perfil predeterminado para el usuario de la base de datos. El usuario de la base de datos solo puede tener un perfil predeterminado. *is_default* es **bits**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento almacenado cambia si el perfil especificado es el perfil predeterminado para el usuario de la base de datos. El usuario de la base de datos solo puede tener un perfil privado predeterminado.  
  
 Cuando el nombre principal de la asociación es **público** o el identificador principal de la asociación es **0**, este procedimiento almacenado cambia el perfil público. Solo puede haber un perfil público predeterminado.  
  
 Cuando **@is_default** es '**1**' y la entidad de seguridad está asociado a más de un perfil, el perfil especificado se convierte en el perfil predeterminado para la entidad de seguridad. El perfil predeterminado anterior sigue estando asociado a la entidad de seguridad, pero ya no es el perfil predeterminado.  
  
 El procedimiento almacenado **sysmail_update_principalprofile_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Configurar un perfil como perfil público predeterminado para una base de datos**  
  
 En el ejemplo siguiente se establece el perfil `General Use Profile` para el perfil público predeterminado para los usuarios de la **msdb** base de datos.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B. Configurar un perfil como perfil privado predeterminado para un usuario**  
  
 En el ejemplo siguiente se establece el perfil `AdventureWorks Administrator` como perfil predeterminado para la entidad de seguridad `ApplicationUser` en el **msdb** base de datos. El perfil ya debe estar asociado a la entidad de seguridad. El perfil predeterminado anterior sigue estando asociado a la entidad de seguridad, pero ya no es el perfil predeterminado.  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
