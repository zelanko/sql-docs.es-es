---
title: sp_adduser (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_adduser
- sp_adduser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adduser
ms.assetid: 61a40eb4-573f-460c-9164-bd1bbfaf8b25
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4f7afe6646fd22ff24aa6aee4e5dcde416420e9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spadduser-transact-sql"></a>sp_adduser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo usuario a la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [CREATE USER](../../t-sql/statements/create-user-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adduser [ @loginame = ] 'login'   
    [ , [ @name_in_db = ] 'user' ]   
    [ , [ @grpname = ] 'role' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@loginame =** ] **'***login***'**  
 Es el nombre del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el inicio de sesión de Windows. *inicio de sesión* es un **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* debe ser una existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o inicio de sesión de Windows.  
  
 [  **@name_in_db =** ] **'***usuario***'**  
 Es el nombre del nuevo usuario de la base de datos. *usuario* es un **sysname**, su valor predeterminado es null. Si *usuario* no se especifica, el nombre del nuevo usuario de base de datos tiene como valor predeterminado el *inicio de sesión* nombre. Especificar *usuario* da al nuevo usuario un nombre de la base de datos distinto del nombre de inicio de sesión de nivel de servidor.  
  
 [  **@grpname =** ] **'***rol***'**  
 Es el rol de base de datos del que el nuevo usuario forma parte automáticamente. *rol* es **sysname**, su valor predeterminado es null. *función* debe ser un rol de base de datos válido en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adduser** también creará un esquema que tiene el nombre del usuario.  
  
 Después de agregar un usuario, utilice las instrucciones GRANT, DENY y REVOKE para definir los permisos que controlan las actividades del usuario.  
  
 Use **sys.server_principals** para mostrar una lista de nombres de inicio de sesión válido.  
  
 Use **sp_helprole** para mostrar una lista de los nombres de función válido. Cuando se especifica un rol, el usuario obtiene automáticamente los permisos definidos para ese rol. Si no se especifica un rol, el usuario obtiene los permisos concedidos en el valor predeterminado **público** rol. Para agregar un usuario a un rol, un valor para el *nombre de usuario* debe proporcionarse. (*nombre de usuario* puede ser el mismo que *login_id*.)  
  
 Usuario **invitado** ya existe en cada base de datos. Al agregar el usuario **invitado** habilitará este usuario, si se deshabilitó anteriormente. De forma predeterminada, usuario **invitado** está deshabilitada en las nuevas bases de datos.  
  
 **sp_adduser** no se puede ejecutar dentro de una transacción definida por el usuario.  
  
 No se puede agregar un **invitado** usuario porque un **invitado** usuario ya existe en cada base de datos. Para habilitar la **invitado** usuario, conceda **invitado** permiso de conexión tal y como se muestra:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 Requiere la propiedad de la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-adding-a-database-user"></a>A. Agregar un usuario de base de datos  
 En el siguiente ejemplo se agrega el usuario de base de datos `Vidur` al rol `Recruiting` existente en la base de datos actual, utilizando el inicio de sesión `Vidur` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente.  
  
```  
EXEC sp_adduser 'Vidur', 'Vidur', 'Recruiting';  
```  
  
### <a name="b-adding-a-database-user-with-the-same-login-id"></a>B. Agregar un usuario de base de datos con el mismo Id. de inicio de sesión  
 En el siguiente ejemplo se agrega el usuario `Arvind` a la base de datos para el inicio de sesión `Arvind` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este usuario pertenece en el valor predeterminado **público** rol.  
  
```  
EXEC sp_adduser 'Arvind';  
```  
  
### <a name="c-adding-a-database-user-with-a-different-name-than-its-server-level-login"></a>C. Agregar un usuario de base de datos con un nombre diferente de su inicio de sesión de nivel de servidor  
 En el siguiente ejemplo se agrega el inicio de sesión `BjornR` de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la base de datos actual que tiene un nombre de usuario `Bjorn`, y agrega un usuario de base de datos `Bjorn` al rol de base de datos `Production`.  
  
```  
EXEC sp_adduser 'BjornR', 'Bjorn', 'Production';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
