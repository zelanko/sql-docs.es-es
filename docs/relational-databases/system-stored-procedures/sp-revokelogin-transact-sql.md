---
title: sp_revokelogin (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6869d96b5fb561328b9eed41c7b5af147b50db10
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sprevokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita las entradas de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para un usuario de Windows o el grupo creado mediante CREATE LOGIN, **sp_grantlogin**, o **sp_denylogin**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame=**] **'***inicio de sesión***'**  
 Es el nombre del usuario o grupo de Windows. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* puede ser cualquier nombre de usuario de Windows existente o un grupo en el formulario *nombre_equipo*\\*usuario o dominio*\\*usuario*.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_revokelogin** deshabilita las conexiones mediante la cuenta especificada por el *inicio de sesión* parámetro. Los usuarios de Windows que tienen acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por medio de su pertenencia a un grupo de Windows, pueden seguir conectándose como parte del grupo aunque se les deniegue el acceso individual. De forma similar, si la *inicio de sesión* parámetro especifica el nombre de un grupo de Windows, los miembros de ese grupo que han sido por separado conceden acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todavía podrán conectarse.  
  
 Por ejemplo, si el usuario de Windows **ADVWORKS\john** es un miembro del grupo de Windows **ADVWORKS\Admins**, y **sp_revokelogin** revoca el acceso de `ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 Usuario **ADVWORKS\john** todavía puede conectarse si **ADVWORKS\Admins** se ha concedido acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma similar, si el grupo de Windows **ADVWORKS\Admins** tiene el acceso al pero **ADVWORKS\john** se concede acceso, **ADVWORKS\john** todavía se pueden conectar.  
  
 Use **sp_denylogin** evitar explícitamente que los usuarios conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de su pertenencia a grupos de Windows.  
  
 **sp_revokelogin** no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita las entradas de inicio de sesión del usuario de Windows `Corporate\MollyA`.  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 O bien  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguridad almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [QUITAR el inicio de sesión &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
