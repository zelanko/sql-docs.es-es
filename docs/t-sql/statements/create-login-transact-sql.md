---
title: CREATE LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
caps.latest.revision: 101
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 6d788da4f619feebd27919d8a34ec81de4a923f4
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452709"
---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)

Crea un inicio de sesión para SQL Server, SQL Database, SQL Data Warehouse o bases de datos de Almacenamiento de datos paralelos. Haga clic en una de las pestañas siguientes para obtener la sintaxis, argumentos, comentarios, permisos y ejemplos para una versión concreta.

Para obtener más información sobre las convenciones de sintaxis, vea [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).
 
# <a name="sql-servertabsqlserver"></a>[SQL Server](#tab/sqlserver)
  
## <a name="syntax"></a>Sintaxis 
  
```  
-- Syntax for SQL Server  
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }  
  
<option_list1> ::=   
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
    SID = sid  
    | DEFAULT_DATABASE = database      
    | DEFAULT_LANGUAGE = language  
    | CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
    | CREDENTIAL = credential_name   
  
<sources> ::=  
    WINDOWS [ WITH <windows_options>[ ,... ] ]  
    | CERTIFICATE certname  
    | ASYMMETRIC KEY asym_key_name  
  
<windows_options> ::=        
    DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
```  
  
## <a name="arguments"></a>Argumentos  
*login_name*  
Especifica el nombre del inicio de sesión que se va a crear. Hay cuatro tipos de inicio de sesión: de SQL Server, de Windows, asignado a un certificado y asignado a una clave asimétrica. Cuando crea inicios de sesión que se asignan desde una cuenta de dominio de Windows, debe utilizar el nombre de inicio de sesión de usuario anterior a Windows 2000 con el formato[\<domainName>\\<login_name>]. No puede utilizar un UPN con el formato login_name@DomainName. Vea el ejemplo D más adelante en este artículo. Los inicios de sesión con autenticación son del tipo **sysname**, deben seguir las reglas de los [Identificadores](http://msdn.microsoft.com/library/ms175874.aspx) y no pueden contener "**\\**". Los inicios de sesión de Windows pueden contener un carácter '**\\**”. Los inicios de sesión basados en usuarios de Active Directory se limitan a nombres de menos de 21 caracteres. 

PASSWORD **="***contraseña***"* Solo se aplica a inicios de sesión de SQL Server. Especifica la contraseña del inicio de sesión que se está creando. Debe utilizar siempre una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de SQL Server 2012 (11.x), la información de la contraseña almacenada se calcula mediante SHA-512 de la contraseña cifrada con sal. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 
  
PASSWORD **=***hashed_password*  
Solo se aplica a la palabra clave HASHED. Especifica el valor con hash de la contraseña para el inicio de sesión que se está creando. 
  
HASHED Solo se aplica a inicios de sesión de SQL Server. Especifica que la contraseña especificada después del argumento PASSWORD ya tiene aplicado el algoritmo hash. Si no se selecciona esta opción, se aplicará el algoritmo hash a la cadena especificada como contraseña antes de almacenarla en la base de datos. Esta opción solo se debería utilizar para migrar las bases de datos de un servidor a otro. No utilice la opción HASHED para crear nuevos inicios de sesión. La opción HASHED no se puede usar con los valores hash creados con SQL 7 o una versión anterior.

MUST_CHANGE solo se aplica a inicios de sesión de SQL Server. Si se incluye esta opción, SQL Server solicita al usuario una contraseña nueva la primera vez que se use el inicio de sesión nuevo. 
  
CREDENTIAL **=***credential_name*  
Nombre de una credencial que se debe asignar al nuevo inicio de sesión de SQL Server. La credencial debe existir en la base de datos. Actualmente esta opción solo vincula la credencial a un inicio de sesión. Las credenciales no se pueden asignar al inicio de sesión del administrador del sistema (sa). 
  
SID = *sid*  
Se usa para volver a crear un inicio de sesión. Solo se aplica a inicios de sesión con autenticación de SQL Server, no a los de Windows. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. SID del inicio de sesión de SQL Server: un valor literal (**binary(16)**) de 16 bytes basado en un GUID. Por ejemplo, `SID = 0x14585E90117152449347750164BA00A7`. 
  
DEFAULT_DATABASE **=***database*  
Especifica la base de datos predeterminada que debe asignarse al inicio de sesión. Si no se incluye esta opción, el valor predeterminado es master. 
  
DEFAULT_LANGUAGE **=***language*  
Especifica el idioma predeterminado que debe asignarse al inicio de sesión. Si no se incluye esta opción, el idioma predeterminado es el del servidor. Si el idioma predeterminado del servidor se cambia más tarde, el del inicio de sesión se mantiene igual. 
  
CHECK_EXPIRATION **=** { ON | **OFF** }  
Solo se aplica a inicios de sesión de SQL Server. Especifica si debe aplicarse la directiva de caducidad de contraseñas en este inicio de sesión. El valor predeterminado es OFF. 
  
CHECK_POLICY **=** { **ON** | OFF }  
Solo se aplica a inicios de sesión de SQL Server. Especifica que se deben aplicar las directivas de contraseñas de Windows en el equipo en el que se ejecuta SQL Server para este inicio de sesión. El valor predeterminado es ON. 
  
Si la directiva de Windows requiere contraseñas seguras, las contraseñas deben tener al menos tres de las cuatro siguientes características:  
  
- Un carácter en mayúscula (A-Z). 
- Un carácter en minúsculas (a-z). 
- Un dígito (0-9). 
- Uno de los caracteres no alfanuméricos, como un espacio, _, @, *, ^, %, !, $, # o &. 
  
WINDOWS  
Especifica que el inicio de sesión se asigna a un inicio de sesión de Windows. 
  
CERTIFICATE *certname*  
Especifica el nombre de un certificado al que asociar este inicio de sesión. Este certificado debe existir en la base de datos maestra. 
  
ASYMMETRIC KEY *asym_key_name*  
Especifica el nombre de una clave asimétrica a la que asociar este inicio de sesión. Esta clave debe existir en la base de datos maestra. 
  
## <a name="remarks"></a>Notas  
- En las contraseñas se distingue entre mayúsculas y minúsculas.
- La aplicación previa del algoritmo hash a las contraseñas solo se admite en la creación de inicios de SQL Server.
- Si se especifica MUST_CHANGE, CHECK_EXPIRATION y CHECK_POLICY, deben establecerse en ON. Si no es así, la instrucción producirá un error.
- No se admite la combinación de CHECK_POLICY = OFF y CHECK_EXPIRATION = ON.
- Cuando CHECK_POLICY se establece en OFF, *lockout_time* se restablece y CHECK_EXPIRATION se establece en OFF. 
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION y CHECK_POLICY solo se aplican en Windows Server 2003 y versiones posteriores. Para obtener más información, vea [Password Policy](../../relational-databases/security/password-policy.md). 
  
- Los inicios de sesión creados con certificados o claves asimétricas solo se usan para la firma del código. No se pueden usar para conectarse a SQL Server. Solo puede crear un inicio de sesión desde un certificado o clave asimétrica cuando este certificado o clave asimétrica ya exista en la base de datos maestra. 
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](http://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- El [modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md) del servidor debe coincidir con el tipo de inicio de sesión para permitir el acceso.
- Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="permissions"></a>Permisos  
- Solo los usuarios con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al rol fijo de servidor **securityadmin** pueden crear inicios de sesión. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles.
- Si se utiliza la opción **CREDENTIAL** , también será necesario el permiso **ALTER ANY CREDENTIAL** en el servidor. 
  
## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Server, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
 - Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
  
 - Cree un rol de servidor definido por el usuario mediante [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** ... **ADD MEMBER** para agregar el nuevo inicio de sesión al rol de servidor definido por el usuario. Para obtener más información, vea [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). 
  
 - Utilice **sp_addsrvrolemember** para agregar el inicio de sesión a un rol fijo de servidor. Para obtener más información, vea [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) y [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md). 
  
 - Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md). 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password-that-must-be-changed"></a>B. Crear un inicio de sesión con una contraseña que se debe cambiar
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. La opción `MUST_CHANGE` exige a los usuarios que cambien la contraseña la primera vez que se conecten al servidor. 
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' 
    MUST_CHANGE,  CHECK_EXPIRATION = ON;
GO  
``` 

> [!NOTE]
> La opción MUST_CHANGE no se puede utilizar cuando se ha desactivado CHECK_EXPIRATION.
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. Crear un inicio de sesión asignado a una credencial  
 El ejemplo siguiente crea el inicio de sesión para un usuario determinado, utilizando el de usuario. Este inicio de sesión se asigna a la credencial. 
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. Crear un inicio de sesión desde un certificado  
 En el ejemplo siguiente se crea el inicio de sesión para un usuario determinado a partir de un certificado de master. 
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
```sql
USE MASTER;  
CREATE CERTIFICATE <certificateName>  
    WITH SUBJECT = '<login_name> certificate in master database',  
    EXPIRY_DATE = '12/05/2025';  
GO  
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;  
GO  
```  
  
### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. Crear un inicio de sesión desde una cuenta de dominio de Windows  
 El ejemplo siguiente crea un inicio de sesión a partir de una cuenta de dominio de Windows. 
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
```sql  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. Crear un inicio de sesión de un SID  
 En el ejemplo siguiente primero se crea un inicio de sesión de autenticación de SQL Server y se determina el SID del inicio de sesión. 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 La consulta devuelve 0x241C11948AEEB749B0D22646DB1A19F2 como el SID. La consulta devolverá un valor diferente. Las siguientes instrucciones eliminan el inicio de sesión y luego vuelven a crear el inicio de sesión. Use el SID de la consulta anterior. 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>Ver también  
- [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
- [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
- [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
- [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
# <a name="sql-databasetabsqldb"></a>[SQL Database](#tab/sqldb)
  
## <a name="syntax"></a>Sintaxis 
  
```
-- Syntax for Azure SQL Database  
CREATE LOGIN login_name  
 { WITH <option_list> }  
  
<option_list> ::=   
    PASSWORD = { 'password' }  
    [ , SID = sid ]  
```  

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), esta característica de T-SQL tiene ciertos cambios de comportamiento. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information) para obtener más información sobre los cambios de comportamiento de T-SQL.
  
## <a name="arguments"></a>Argumentos  
*login_name*  
Especifica el nombre del inicio de sesión que se va a crear. Azure SQL Database solo admite los inicios de sesión SQL. 

PASSWORD **="** contraseña**"*  
Especifica la contraseña del inicio de sesión SQL que se está creando. Debe utilizar siempre una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la información de la contraseña almacenada se calcula con las funciones SHA-512 de la contraseña salada. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 

SID = *sid*  
Se usa para volver a crear un inicio de sesión. Solo se aplica a inicios de sesión con autenticación de SQL Server, no a los de Windows. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. Para SQL Database, esto es un literal (**binary(32)**) de 32 bytes que consta de `0x01060000000000640000000000000000` más 16 bytes que representan un GUID. Por ejemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`. 
  
## <a name="remarks"></a>Notas  
- En las contraseñas se distingue entre mayúsculas y minúsculas.
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](http://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- El [modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md) del servidor debe coincidir con el tipo de inicio de sesión para permitir el acceso.
    - Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).
  
## <a name="login"></a>Login

### <a name="sql-database-logins"></a>Inicios de sesión en SQL Database
La instrucción **CREATE LOGIN** debe ser la única de un lote. 
  
En algunos métodos de conexión con SQL Database, como **sqlcmd**, debe anexar el nombre del servidor de SQL Database al nombre de inicio de sesión en la cadena de conexión mediante la notación *\<inicio_de_sesión>*@*\<servidor>*. Por ejemplo, si el inicio de sesión es `login1` y el nombre completo del servidor de SQL Database es `servername.database.windows.net`, el parámetro *nombre_de_usuario* de la cadena de conexión debe ser `login1@servername`. Dado que la longitud total del parámetro *username* es de 128 caracteres, *login_name* se limita a 127 caracteres menos la longitud del nombre del servidor. En el ejemplo, `login_name` solo puede tener 117 caracteres porque `servername` es de 10 caracteres. 
  
En SQL Database, debe estar conectado a la base de datos maestra para crear un inicio de sesión. 
  
 Las reglas de SQL Server permiten crear un inicio de sesión con autenticación de SQL Server con el formato \<nombreDeInicioDeSesión>@\<nombreDeServidor>. Si el servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] es **myazureserver** y el inicio de sesión es **myemail@live.com**, debe proporcionar un inicio de sesión como **myemail@live.com@myazureserver**. 
  
En SQL Database, los datos de inicio de sesión necesarios para autenticar una conexión y las reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza regularmente. Para forzar una actualización de la caché de autenticación y garantizar que una base de datos tenga la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md). 
  
 Para obtener más información sobre los inicios de sesión de SQL Database, vea [Administrar bases de datos e inicios de sesión en Microsoft Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins). 
 
## <a name="permissions"></a>Permisos

Solo pueden crear inicios de sesión el inicio de sesión de entidad de seguridad a nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos `loginmanager` en la base de datos maestra. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles.

## <a name="logins"></a>Inicios de sesión
- Debe tener el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al rol fijo de servidor **securityadmin**. Solo la cuenta de Azure Active Directory (Azure AD) con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al permiso securityadmin pueden ejecutar este comando.
- Debe ser un miembro de Azure AD en el mismo directorio que se use para el servidor lógico de Azure SQL.
  
## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Database, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
- Para conectarse a una base de datos, cree un usuario de base de datos para el inicio de sesión en esa base de datos. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
- Para conceder permisos a un usuario en una base de datos, use la instrucción **ALTER SERVER ROLE** ... **ADD MEMBER** para agregar el uso a uno de los roles de base de datos integrado o a un rol personalizado, o bien conceda los permisos al usuario directamente mediante la instrucción [GRANT]((../../t-sql/statements/grant-transact-sql.md). Para obtener más información, vea [Roles no administradores](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles y la instrucción [GRANT](grant-transact-sql.md).
- Para conceder permisos de todo el servidor, cree un usuario de base de datos en la base de datos maestra y use la instrucción **ALTER SERVER ROLE** ... **ADD MEMBER** para agregar el uso a uno de los roles de servidor de administración. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) y [Roles de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).
- Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-from-a-sid"></a>B. Crear un inicio de sesión de un SID  
 En el ejemplo siguiente primero se crea un inicio de sesión de autenticación de SQL Server y se determina el SID del inicio de sesión. 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 La consulta devuelve 0x241C11948AEEB749B0D22646DB1A19F2 como el SID. La consulta devolverá un valor diferente. Las siguientes instrucciones eliminan el inicio de sesión y luego vuelven a crear el inicio de sesión. Use el SID de la consulta anterior. 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
# <a name="sql-data-warehousetabsqldw"></a>[SQL Data Warehouse](#tab/sqldw)
  
## <a name="syntax"></a>Sintaxis 
  
```
-- Syntax for Azure SQL Data Warehouse  
CREATE LOGIN login_name  
 { WITH <option_list> }  
  
<option_list> ::=   
    PASSWORD = { 'password' }  
    [ , SID = sid ]  
```  
  
## <a name="arguments"></a>Argumentos  
*login_name*  
Especifica el nombre del inicio de sesión que se va a crear. Azure SQL Database solo admite los inicios de sesión SQL. 

PASSWORD **="** contraseña**"*  
Especifica la contraseña del inicio de sesión SQL que se está creando. Debe utilizar siempre una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la información de la contraseña almacenada se calcula con las funciones SHA-512 de la contraseña salada. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 

 SID = *sid*  
 Se usa para volver a crear un inicio de sesión. Solo se aplica a inicios de sesión con autenticación de SQL Server, no a los de Windows. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. Para SQL Data Warehouse, esto es un literal (**binary(32)**) de 32 bytes que consta de `0x01060000000000640000000000000000` más 16 bytes que representan un GUID. Por ejemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`. 
  
## <a name="remarks"></a>Notas  
- En las contraseñas se distingue entre mayúsculas y minúsculas.
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](http://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- El [modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md) del servidor debe coincidir con el tipo de inicio de sesión para permitir el acceso.
    - Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).
  
## <a name="logins"></a>Inicios de sesión

La instrucción **CREATE LOGIN** debe ser la única de un lote. 
  
En algunos métodos de conexión con SQL Data Warehouse, como **sqlcmd**, debe anexar el nombre del servidor de SQL Data Warehouse al nombre de inicio de sesión en la cadena de conexión mediante la notación *\<inicio_de_sesión>*@*\<servidor>*. Por ejemplo, si el inicio de sesión es `login1` y el nombre completo del servidor de SQL Data Warehouse es `servername.database.windows.net`, el parámetro *nombre_de_usuario* de la cadena de conexión debe ser `login1@servername`. Dado que la longitud total del parámetro *username* es de 128 caracteres, *login_name* se limita a 127 caracteres menos la longitud del nombre del servidor. En el ejemplo, `login_name` solo puede tener 117 caracteres porque `servername` es de 10 caracteres. 
  
En SQL Data Warehouse, debe estar conectado a la base de datos maestra para crear un inicio de sesión. 
  
 Las reglas de SQL Server permiten crear un inicio de sesión con autenticación de SQL Server con el formato \<nombreDeInicioDeSesión>@\<nombreDeServidor>. Si el servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] es **myazureserver** y el inicio de sesión es **myemail@live.com**, debe proporcionar un inicio de sesión como **myemail@live.com@myazureserver**. 
  
En SQL Data Warehouse, los datos de inicio de sesión necesarios para autenticar una conexión y las reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza regularmente. Para forzar una actualización de la caché de autenticación y garantizar que una base de datos tenga la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md). 
  
 Para obtener más información sobre los inicios de sesión de Azure SQL Data Warehouse, vea [Administrar bases de datos e inicios de sesión en Microsoft Azure SQL Database](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins). 
 
## <a name="permissions"></a>Permisos

Solo pueden crear inicios de sesión el inicio de sesión de entidad de seguridad a nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos `loginmanager` en la base de datos maestra. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles.

## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Data Warehouse, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
- Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md).
- Para conceder permisos a un usuario en una base de datos, use la instrucción **ALTER SERVER ROLE** ... **ADD MEMBER** para agregar el uso a uno de los roles de base de datos integrado o a un rol personalizado, o bien conceda los permisos al usuario directamente mediante la instrucción [GRANT](grant-transact-sql.md). Para obtener más información, vea [Roles no administradores](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles y la instrucción [GRANT](grant-transact-sql.md).
- Para conceder permisos de todo el servidor, cree un usuario de base de datos en la base de datos maestra y use la instrucción **ALTER SERVER ROLE** ... **ADD MEMBER** para agregar el uso a uno de los roles de servidor de administración. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) y [Roles de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).

- Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md). 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-login-from-a-sid"></a>B. Crear un inicio de sesión de un SID  
 En el ejemplo siguiente primero se crea un inicio de sesión de autenticación de SQL Server y se determina el SID del inicio de sesión. 
  
```sql  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 La consulta devuelve 0x241C11948AEEB749B0D22646DB1A19F2 como el SID. La consulta devolverá un valor diferente. Las siguientes instrucciones eliminan el inicio de sesión y luego vuelven a crear el inicio de sesión. Use el SID de la consulta anterior. 
  
```sql  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
# <a name="sql-parallel-data-warehousetabsqlpdw"></a>[Almacenamiento de datos paralelos de SQL](#tab/sqlpdw)
  
## <a name="syntax"></a>Sintaxis 
  
```
-- Syntax for Parallel Data Warehouse  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list> [ ,... ] ]  
  
<option_list> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  

## <a name="arguments"></a>Argumentos  
*login_name*  
Especifica el nombre del inicio de sesión que se va a crear. Hay cuatro tipos de inicio de sesión: de SQL Server, de Windows, asignado a un certificado y asignado a una clave asimétrica. Cuando crea inicios de sesión que se asignan desde una cuenta de dominio de Windows, debe utilizar el nombre de inicio de sesión de usuario anterior a Windows 2000 con el formato[\<domainName>\\<login_name>]. No puede utilizar un UPN con el formato login_name@DomainName. Vea el ejemplo D más adelante en este artículo. Los inicios de sesión con autenticación son del tipo **sysname**, deben seguir las reglas de los [Identificadores](http://msdn.microsoft.com/library/ms175874.aspx) y no pueden contener "**\\**". Los inicios de sesión de Windows pueden contener un carácter '**\\**”. Los inicios de sesión basados en usuarios de Active Directory se limitan a nombres de menos de 21 caracteres. 

PASSWORD **="***contraseña***"* Solo se aplica a inicios de sesión de SQL Server. Especifica la contraseña del inicio de sesión que se está creando. Debe utilizar siempre una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de SQL Server 2012 (11.x), la información de la contraseña almacenada se calcula mediante SHA-512 de la contraseña cifrada con sal. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 
  
MUST_CHANGE Solo se aplica a inicios de sesión de SQL Server. Si se incluye esta opción, SQL Server solicita al usuario una contraseña nueva la primera vez que se use el inicio de sesión nuevo. 
  
CHECK_EXPIRATION **=** { ON | **OFF** }  
Solo se aplica a inicios de sesión de SQL Server. Especifica si debe aplicarse la directiva de caducidad de contraseñas en este inicio de sesión. El valor predeterminado es OFF. 
  
CHECK_POLICY **=** { **ON** | OFF }  
Solo se aplica a inicios de sesión de SQL Server. Especifica que se deben aplicar las directivas de contraseñas de Windows en el equipo en el que se ejecuta SQL Server para este inicio de sesión. El valor predeterminado es ON. 
  
Si la directiva de Windows requiere contraseñas seguras, las contraseñas deben tener al menos tres de las cuatro siguientes características:  
  
- Un carácter en mayúscula (A-Z). 
- Un carácter en minúsculas (a-z). 
- Un dígito (0-9). 
- Uno de los caracteres no alfanuméricos, como un espacio, _, @, *, ^, %, !, $, # o &. 
  
WINDOWS  
Especifica que el inicio de sesión se asigna a un inicio de sesión de Windows. 
  
## <a name="remarks"></a>Notas  
- En las contraseñas se distingue entre mayúsculas y minúsculas.
- Si se especifica MUST_CHANGE, CHECK_EXPIRATION y CHECK_POLICY, deben establecerse en ON. Si no es así, la instrucción producirá un error.
- No se admite la combinación de CHECK_POLICY = OFF y CHECK_EXPIRATION = ON.
- Cuando CHECK_POLICY se establece en OFF, *lockout_time* se restablece y CHECK_EXPIRATION se establece en OFF. 
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION y CHECK_POLICY solo se aplican en Windows Server 2003 y versiones posteriores. Para obtener más información, vea [Password Policy](../../relational-databases/security/password-policy.md). 
  
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](http://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="permissions"></a>Permisos  
Solo los usuarios con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al rol fijo de servidor **securityadmin** pueden crear inicios de sesión. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).https://docs.microsoft.com/en-us/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles.
  
## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Data Warehouse, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
 - Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
  
 - Cree un rol de servidor definido por el usuario mediante [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** ... **ADD MEMBER** para agregar el nuevo inicio de sesión al rol de servidor definido por el usuario. Para obtener más información, vea [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). 
  
 - Utilice **sp_addsrvrolemember** para agregar el inicio de sesión a un rol fijo de servidor. Para obtener más información, vea [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) y [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md). 
  
 - Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md). 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. Crear un inicio de sesión de autenticación de SQL Server con una contraseña  
 En el ejemplo siguiente se crea el inicio de sesión `Mary7` con la contraseña `A2c3456`. 
  
```sql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. Usar Opciones  
 En el siguiente ejemplo se crea el inicio de sesión `Mary8` con contraseña y algunos de los argumentos opcionales. 
  
```sql  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. Crear un inicio de sesión desde una cuenta de dominio de Windows  
 En el ejemplo siguiente se crea un inicio de sesión a partir de una cuenta de dominio de Windows denominada `Mary` en el dominio `Contoso`. 
  
```sql  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
---  
