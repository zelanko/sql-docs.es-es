---
title: sp_migrate_user_to_contained (Transact-SQL) | Documentos de Microsoft
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
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b6a0b15ff483647a3c102d481d8300ff460ce8c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Convierte a un usuario de base de datos asignado a un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un usuario de base de datos independiente con contraseña. En una base de datos independiente, utilice este procedimiento para quitar las dependencias sobre la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde se instala la base de datos. **sp_migrate_user_to_contained** separa al usuario original [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, para que los valores como contraseña e idioma predeterminado se puedan administrar por separado para la base de datos independiente. **sp_migrate_user_to_contained** puede usarse antes de mover la base de datos independiente a una instancia distinta de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para eliminar las dependencias en la actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión de la instancia.  
  
 **Tenga en cuenta** este procedimiento sólo se utiliza en una base de datos independiente. Para más información, consulte [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@username =** ] **N'***usuario***'**  
 Nombre de un usuario en la base de datos independiente actual asignado a un inicio de sesión autenticado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El valor es **sysname**, su valor predeterminado es **NULL**.  
  
 [ **@rename =** ] **N'***copy_login_name***'** | **N'** *keep_name***'**  
 Cuando un usuario de base de datos basado en un inicio de sesión tiene un nombre de usuario diferente que el nombre de inicio de sesión, utilice *keep_name* para conservar el nombre de usuario de base de datos durante la migración. Use *copy_login_name* para crear el nuevo usuario de base de datos independiente con el nombre del inicio de sesión, en lugar del usuario. Cuando un usuario de la base de datos basado en inicio de sesión tiene el mismo nombre de usuario que el nombre de inicio de sesión, ambas opciones crean el usuario de la base de datos independiente sin cambiar el nombre.  
  
 [ **@disablelogin =** ] **N'***disable_login***'** | **N'** *do_not_disable_login***'**  
 *disable_login* deshabilita el inicio de sesión en la base de datos maestra. Para conectarse cuando se deshabilita el inicio de sesión, la conexión debe proporcionar el nombre de la base de datos independiente como el **catálogo inicial** como parte de la cadena de conexión.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_migrate_user_to_contained** crea el usuario de base de datos independiente con contraseña, independientemente de las propiedades o los permisos del inicio de sesión. Por ejemplo, el procedimiento puede tener éxito si el inicio de sesión está deshabilitado o si el usuario tiene denegado el **conectar** permiso para la base de datos.  
  
 **sp_migrate_user_to_contained** tiene las siguientes restricciones.  
  
-   El nombre de usuario no puede existir ya en la base de datos.  
  
-   Los usuarios integrados, por ejemplo dbo y guest, no se pueden convertir.  
  
-   El usuario no puede especificarse en el **EXECUTE AS** cláusula de un procedimiento almacenado firmado.  
  
-   El usuario no puede poseer un procedimiento almacenado que incluye el **EXECUTE AS OWNER** cláusula.  
  
-   **sp_migrate_user_to_contained** no se puede usar en una base de datos del sistema.  
  
## <a name="security"></a>Seguridad  
 Al realizar la migración de los usuarios, tenga el cuidado de no deshabilitar o eliminar todos los inicios de sesión de administrador de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se eliminan todos los inicios de sesión, vea [conectar a SQL Server al sistema los administradores no tienen acceso](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Si el **BUILTIN\Administrators** inicio de sesión está presente, los administradores pueden conectar iniciando su aplicación mediante la **ejecutar como administrador** opción.  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso **CONTROL SERVER** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-migrating-a-single-user"></a>A. Realizar la migración de un usuario único  
 En el siguiente ejemplo, se realiza una migración de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominado `Barry` a un usuario de base de datos independiente con contraseña. El ejemplo conserva el nombre de usuario y mantiene el inicio de sesión como habilitado.  
  
```tsql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. Realizar la migración de todos los usuarios de la base de datos con inicios de sesión a usuarios de base de datos independiente sin inicio de sesión  
 En el siguiente ejemplo, se realiza la migración de todos los usuarios basados en inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usuarios de base de datos independiente con contraseñas. En el ejemplo se excluyen los inicios de sesión que no están habilitados. El ejemplo se debe ejecutar en la base de datos independiente.  
  
```tsql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [Bases de datos independientes](../../relational-databases/databases/contained-databases.md)  
  
  
