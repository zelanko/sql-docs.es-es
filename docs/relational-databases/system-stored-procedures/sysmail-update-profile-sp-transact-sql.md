---
title: sysmail_update_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: d2b1616fdf7b690d61c6a2605cc15da2508a3fb9
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534667"
---
# <a name="sysmailupdateprofilesp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la descripción o el nombre de un perfil del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` El identificador de perfil para la actualización. *profile_id* es **int**, su valor predeterminado es null. Al menos uno de *profile_id* o *profile_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre del perfil.  
  
`[ @profile_name = ] 'profile_name'` El nombre del perfil que desea actualizar o el nuevo nombre para el perfil. *nombre_perfil* es **sysname**, su valor predeterminado es null. Al menos uno de *profile_id* o *profile_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre del perfil.  
  
`[ @description = ] 'description'` La nueva descripción para el perfil. *descripción* es **nvarchar (256)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Si se especifican los dos (el Id. de perfil y el nombre de perfil), el procedimiento cambia el nombre del perfil por el nombre proporcionado y actualiza su descripción. Si solo se proporciona uno de estos argumentos, el procedimiento actualiza la descripción del perfil.  
  
 El procedimiento almacenado **sysmail_update_profile_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
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
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
