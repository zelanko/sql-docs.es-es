---
title: sp_approlepassword (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_approlepassword
- sp_approlepassword_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_approlepassword
ms.assetid: 7967dc0b-bee2-4c63-b8e9-1c3ce2f5db2a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06198932c654bf7e8d855b4a008b3de3401dda1c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131515"
---
# <a name="spapprolepassword-transact-sql"></a>sp_approlepassword (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la contraseña de un rol de aplicación en la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER APPLICATION ROLE](../../t-sql/statements/alter-application-role-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_approlepassword [ @rolename= ] 'role' , [ @newpwd = ] 'password'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'**_rol_**'**  
 Es el nombre del rol de aplicación. *rol* es **sysname**, no tiene ningún valor predeterminado. *rol* debe existir en la base de datos actual.  
  
 [  **@newpwd =** ] **'**_contraseña_**'**  
 Es la nueva contraseña para el rol de aplicación. *contraseña* es **sysname**, no tiene ningún valor predeterminado. *contraseña* no puede ser NULL.  
  
> [!IMPORTANT]  
>  No utilice una contraseña NULL. Utilice una contraseña segura. Para obtener más información, consulte [Strong Passwords](../../relational-databases/security/strong-passwords.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_approlepassword** no se puede ejecutar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY APPLICATION ROLE en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se establece la contraseña para el rol de aplicación `PayrollAppRole` en `B3r12-36`.  
  
```  
EXEC sp_approlepassword 'PayrollAppRole', '''B3r12-36';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_addapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
