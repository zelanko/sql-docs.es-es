---
title: sysmail_update_profile_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs: TSQL
helpviewer_keywords: sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8ac35d2b28b6a85759e322d0248da044452a46c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailupdateprofilesp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la descripción o el nombre de un perfil del Correo electrónico de base de datos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id**  =] *profile_id*  
 Id. de perfil para la actualización. *profile_id* es **int**, su valor predeterminado es null. Al menos uno de *profile_id* o *profile_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre del perfil.  
  
 [  **@profile_name**  =] **'***profile_name***'**  
 Nombre del perfil que se va a actualizar o nombre nuevo del perfil. *profile_name* es **sysname**, su valor predeterminado es null. Al menos uno de *profile_id* o *profile_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre del perfil.  
  
 [  **@description**  =] **'***descripción***'**  
 La nueva descripción del perfil. *descripción* es **nvarchar (256)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Si se especifican los dos (el Id. de perfil y el nombre de perfil), el procedimiento cambia el nombre del perfil por el nombre proporcionado y actualiza su descripción. Si solo se proporciona uno de estos argumentos, el procedimiento actualiza la descripción del perfil.  
  
 El procedimiento almacenado **sysmail_update_profile_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Cambiar la descripción de un perfil**  
  
 En el ejemplo siguiente se cambia la descripción del perfil denominado `AdventureWorks Administrator` en el **msdb** base de datos.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **B. Cambiar el nombre y la descripción de un perfil**  
  
 En este ejemplo se cambia el nombre y la descripción del perfil con el Id. de perfil `750`.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Correo electrónico de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
