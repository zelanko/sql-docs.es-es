---
title: MODIFICAR el rol de servidor (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_ROLE_TSQL
- ALTER SERVER ROLE
dev_langs: TSQL
helpviewer_keywords:
- SERVER ROLE, ALTER
- ALTER SERVER ROLE statement
ms.assetid: 7a4db7bb-c442-4e12-9a8a-114da5bc7710
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7ce5b5223f5c755c89cb3e105ceb6517087d699f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-server-role-transact-sql"></a>ALTER SERVER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-pdw-md.md)]

Cambia la pertenencia de un rol de servidor o cambia el nombre de un rol de servidor definido por el usuario. No se puede cambiar el nombre de los roles fijos de servidor.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
ALTER SERVER ROLE server_role_name   
{  
    [ ADD MEMBER server_principal ]  
  | [ DROP MEMBER server_principal ]  
  | [ WITH NAME = new_server_role_name ]  
} [ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER SERVER ROLE  server_role_name  ADD MEMBER login;  
  
ALTER SERVER ROLE  server_role_name  DROP MEMBER login;  
```  
  
## <a name="arguments"></a>Argumentos  
*nombre_del_rol_de_servidor*  
Nombre del rol de servidor que se va a cambiar.  
  
Agregar miembro *entidadseguridadservidor*  
Agrega la entidad de seguridad del servidor especificada al rol de servidor. *entidadseguridadservidor* puede ser un inicio de sesión o un rol de servidor definidos por el usuario. *entidadseguridadservidor* no puede ser un rol fijo de servidor, un rol de base de datos o sa.  
  
DROP MEMBER *entidadseguridadservidor*  
Quita la entidad de seguridad del servidor especificada del rol de servidor. *entidadseguridadservidor* puede ser un inicio de sesión o un rol de servidor definidos por el usuario. *entidadseguridadservidor* no puede ser un rol fijo de servidor, un rol de base de datos o sa.  
  
CON el nombre  **=**  *nuevonombrerolservidor*  
Especifica el nuevo nombre del rol de servidor definido por el usuario. Este nombre no puede existir ya en el servidor.  
  
## <a name="remarks"></a>Comentarios  
El cambio de nombre de un rol de servidor definido por el usuario no cambia el número de identificación, el propietario ni los permisos del rol.  
  
Para cambiar la pertenencia a roles, `ALTER SERVER ROLE` reemplaza sp_addsrvrolemember y sp_dropsrvrolemember. Estos procedimientos almacenados están desusados.  
  
Puede ver los roles de servidor si consulta las vistas de catálogo `sys.server_role_members` y `sys.server_principals`.  
  
Para cambiar el propietario de un rol de servidor definidos por el usuario, utilice [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
Requiere `ALTER ANY SERVER ROLE` permiso en el servidor para cambiar el nombre de un rol de servidor definidos por el usuario.  
  
**Roles fijos de servidor**  
  
Para agregar un miembro a un rol fijo de servidor, debe ser miembro de ese rol fijo de servidor o del rol fijo de servidor `sysadmin`.  
  
> [!NOTE]  
>  El `CONTROL SERVER` y `ALTER ANY SERVER ROLE` permisos no son suficientes para ejecutar `ALTER SERVER ROLE` para un rol fijo de servidor, y `ALTER` no se puede conceder el permiso en un rol fijo de servidor.  
  
**Roles de servidor definido por el usuario**  
  
Para agregar un miembro a un rol de servidor definidos por el usuario, debe ser miembro de la `sysadmin` rol fijo de servidor o tiene `CONTROL SERVER` o `ALTER ANY SERVER ROLE` permiso. O bien debe tener `ALTER` permiso para ese rol.  
  
> [!NOTE]  
>  A diferencia de los roles fijos de servidor, los miembros de un rol de servidor definido por el usuario no disponen inherentemente de permiso para agregar miembros a ese mismo rol.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-name-of-a-server-role"></a>A. Cambiar el nombre de un rol de servidor  
En el siguiente ejemplo se crea un rol de servidor denominado `Product` y, a continuación, se cambia el nombre del rol de servidor a `Production`.  
  
```  
CREATE SERVER ROLE Product ;  
ALTER SERVER ROLE Product WITH NAME = Production ;  
GO  
```  
  
### <a name="b-adding-a-domain-account-to-a-server-role"></a>B. Agregar una cuenta de dominio a un rol de servidor  
En el ejemplo siguiente se agrega una cuenta de dominio denominada `adventure-works\roberto0` para el rol de servidor definido por el usuario denominado `Production`.  
  
```  
ALTER SERVER ROLE Production ADD MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="c-adding-a-sql-server-login-to-a-server-role"></a>C. Agregar un inicio de sesión de SQL Server a un rol de servidor  
En el ejemplo siguiente se agrega un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión denominado `Ted` a la `diskadmin` rol fijo de servidor.  
  
```  
ALTER SERVER ROLE diskadmin ADD MEMBER Ted ;  
GO  
```  
  
### <a name="d-removing-a-domain-account-from-a-server-role"></a>D. Quitar una cuenta de dominio de un rol de servidor  
En el ejemplo siguiente se quita una cuenta de dominio denominada `adventure-works\roberto0` desde el rol de servidor definido por el usuario denominado `Production`.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER [adventure-works\roberto0] ;  
```  
  
### <a name="e-removing-a-sql-server-login-from-a-server-role"></a>E. Quitar un inicio de sesión de SQL Server de un rol de servidor  
En el ejemplo siguiente se quita el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión `Ted` desde el `diskadmin` rol fijo de servidor.  
  
```  
ALTER SERVER ROLE Production DROP MEMBER Ted ;  
GO  
```  
  
### <a name="f-granting-a-login-the-permission-to-add-logins-to-a-user-defined-server-role"></a>F. Conceder a un inicio de sesión el permiso para agregar inicios de sesión a un rol de servidor definido por el usuario  
En el siguiente ejemplo se permite a `Ted` agregar otros inicio de sesión al rol de servidor definido por el usuario denominado `Production`.  
  
```  
GRANT ALTER ON SERVER ROLE::Production TO Ted ;  
GO  
```  
  
### <a name="g-to-view-role-membership"></a>G. Para ver la pertenencia al rol  
Para ver la pertenencia al rol, use la **rol de servidor (miembros)** página [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o ejecute la consulta siguiente:  
  
```  
SELECT SRM.role_principal_id, SP.name AS Role_Name,   
SRM.member_principal_id, SP2.name  AS Member_Name  
FROM sys.server_role_members AS SRM  
JOIN sys.server_principals AS SP  
    ON SRM.Role_principal_id = SP.principal_id  
JOIN sys.server_principals AS SP2   
    ON SRM.member_principal_id = SP2.principal_id  
ORDER BY  SP.name,  SP2.name  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-basic-syntax"></a>H. Sintaxis básica  
En el ejemplo siguiente se agrega el inicio de sesión `Anna` a la `LargeRC` rol de servidor.  
  
```  
ALTER SERVER ROLE LargeRC ADD MEMBER Anna;  
```  
  
### <a name="i-remove-a-login-from-a-resource-class"></a>I. Quitar un inicio de sesión de una clase de recursos.  
En el ejemplo siguiente se quita la pertenencia de Ana el `LargeRC` rol de servidor.  
  
```  
ALTER SERVER ROLE LargeRC DROP MEMBER Anna;  
```  
  
## <a name="see-also"></a>Vea también  
[Crear rol de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
[QUITAR el rol de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
[Crear rol &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
[ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
[ELIMINAR rol &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
[Seguridad almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
[Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
[Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
[Sys.server_role_members &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
[sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
