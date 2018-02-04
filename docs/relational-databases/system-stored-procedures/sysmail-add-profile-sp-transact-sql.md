---
title: sysmail_add_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6295b1f239f136c43e00e047186ce408ab9a4a93
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuevo perfil de Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_name**  =] **'***profile_name***'**  
 Nombre del nuevo perfil. *profile_name* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@description**  =] **'***descripción***'**  
 Descripción opcional del nuevo perfil. *descripción* es **nvarchar (256)**, no tiene ningún valor predeterminado.  
  
 [ **@profile_id** = ] *new_profile_id***OUTPUT**  
 Devuelve el identificador del nuevo perfil. *new_profile_id* es **int**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Un perfil de Correo electrónico de base de datos contiene cualquier número de cuentas de Correo electrónico de base de datos. Los procedimientos almacenados de Correo electrónico de base de datos pueden hacer referencia a un perfil por el nombre o por el Id. del perfil generado por este procedimiento. Para obtener más información acerca de cómo agregar una cuenta a un perfil, vea [sysmail_add_profileaccount_sp &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md).  
  
 El nombre del perfil y la descripción se pueden cambiar con el procedimiento almacenado **sysmail_update_profile_sp**, mientras que el identificador de perfil permanece constante durante la vida del perfil.  
  
 El nombre del perfil debe ser único para el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] de Microsoft o el procedimiento almacenado devuelve un error.  
  
 El procedimiento almacenado **sysmail_add_profile_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Crear un nuevo perfil**  
  
 En el ejemplo siguiente se crea un nuevo perfil de Correo electrónico de base de datos denominado `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. Crear un nuevo perfil y guardar el Id. del perfil en una variable**  
  
 En el ejemplo siguiente se crea un nuevo perfil de Correo electrónico de base de datos denominado `AdventureWorks Administrator`. En el ejemplo se almacena el Id. del perfil en la variable `@profileId` y se devuelve un conjunto de resultados que contiene el Id. del nuevo perfil.  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Correo electrónico de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
