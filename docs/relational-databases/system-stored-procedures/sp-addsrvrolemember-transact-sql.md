---
title: sp_addsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addsrvrolemember
- sp_addsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addsrvrolemember
ms.assetid: 777f0e09-8ee5-4cb2-a3ac-939d02c3cd22
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c927bdff462922d1846188366fbb92ce0d3663c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022417"
---
# <a name="sp_addsrvrolemember-transact-sql"></a>sp_addsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un inicio de sesión como miembro de un rol fijo de servidor.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, use [ALTER Server role](../../t-sql/statements/alter-server-role-transact-sql.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addsrvrolemember [ @loginame= ] 'login'   
    , [ @rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame **=** ] **'**_Inicio de sesión_**'**  
 Es el nombre del inicio de sesión que se va a agregar al rol fijo de servidor. *login* es de **tipo sysname**y no tiene ningún valor predeterminado. el *Inicio* de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ser un inicio de sesión de o un inicio de sesión de Windows. Si el inicio de sesión de Windows no tiene acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todavía, se le concede el acceso automáticamente.  
  
 [ @rolename **=** ] **'**_role_**'**  
 Es el nombre del rol fijo de servidor al que se va a agregar el inicio de sesión. *role* es de **tipo sysname, su**valor predeterminado es NULL y debe ser uno de los siguientes valores:  
  
-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin  

## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Cuando se agrega un inicio de sesión a un rol fijo de servidor, el inicio de sesión obtiene los permisos asociados a dicho rol.  
  
 La pertenencia a roles de los inicios de sesión sa y public no se puede cambiar.  
  
 Para agregar miembros a roles fijos de base de datos o a roles definidos por el usuario, utilice sp_addrolemember.  
  
 sp_addsrvrolemember no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol al que se agrega el nuevo miembro.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega el `Corporate\HelenS` inicio de `sysadmin` sesión de Windows al rol fijo de servidor.  
  
```  
EXEC sp_addsrvrolemember 'Corporate\HelenS', 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)  
  
  
