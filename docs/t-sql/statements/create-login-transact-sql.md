---
title: CREATE LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 75c1bb4f7c236f45b94e534ceec2655fc24808df
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2019
ms.locfileid: "53980441"
---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)

Crea un inicio de sesión para SQL Server, SQL Database, SQL Data Warehouse o bases de datos de Almacenamiento de datos paralelos. Haga clic en una de las pestañas siguientes para obtener la sintaxis, argumentos, comentarios, permisos y ejemplos para una versión concreta.

Para obtener más información sobre las convenciones de sintaxis, vea [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). 

## <a name="click-a-product"></a>Haga clic en un producto.

En la siguiente fila, haga clic en cualquier nombre de producto que le interese. Al hacer clic, en esta página web se muestra otro contenido, adecuado para el producto que seleccione.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||||
> |-|-|-|-|-|
> |**_\* SQL Server \*_**|[Servidor lógico de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-current)|[Instancia administrada de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[Almacenamiento de datos<br /> paralelos](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="sql-server"></a>SQL Server

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
Especifica el nombre del inicio de sesión que se va a crear. Hay cuatro tipos de inicios de sesión: inicios de sesión de SQL Server, de Windows, asignados a certificados y asignados a claves asimétricas. Cuando crea inicios de sesión que se asignan desde una cuenta de dominio de Windows, debe utilizar el nombre de inicio de sesión de usuario anterior a Windows 2000 con el formato[\<domainName>\\<login_name>]. No puede utilizar un UPN con el formato login_name@DomainName. Vea el ejemplo D más adelante en este artículo. Los inicios de sesión con autenticación son del tipo **sysname**, deben seguir las reglas de los [Identificadores](../../relational-databases/databases/database-identifiers.md) y no pueden contener "**\\**". Los inicios de sesión de Windows pueden contener un carácter '**\\**”. Los inicios de sesión basados en usuarios de Active Directory se limitan a nombres de menos de 21 caracteres. 

PASSWORD **=**"*contraseña*" Solo se aplica a los inicios de sesión de SQL Server. Especifica la contraseña del inicio de sesión que se está creando. Utilice una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de SQL Server 2012 (11.x), la información de contraseña almacenada se calcula con SHA-512 de la contraseña cifrada con sal. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres de longitud y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 
  
PASSWORD **=** *contraseña\_con_hash*  
Solo se aplica a la palabra clave HASHED. Especifica el valor con hash de la contraseña para el inicio de sesión que se está creando. 
  
HASHED Solo se aplica a inicios de sesión de SQL Server. Especifica que la contraseña especificada después del argumento PASSWORD ya tiene aplicado el algoritmo hash. Si no se selecciona esta opción, se aplicará el algoritmo hash a la cadena especificada como contraseña antes de almacenarla en la base de datos. Esta opción solo se debería utilizar para migrar las bases de datos de un servidor a otro. No utilice la opción HASHED para crear nuevos inicios de sesión. La opción HASHED no se puede usar con los valores hash creados con SQL 7 o una versión anterior.

MUST_CHANGE solo se aplica a inicios de sesión de SQL Server. Si se incluye esta opción, SQL Server solicita al usuario una contraseña nueva la primera vez que se use el inicio de sesión nuevo. 
  
CREDENTIAL **=**_credential\_name_  
Nombre de una credencial que se debe asignar al nuevo inicio de sesión de SQL Server. La credencial debe existir en la base de datos. Actualmente esta opción solo vincula la credencial a un inicio de sesión. Las credenciales no se pueden asignar al inicio de sesión del administrador del sistema (sa). 
  
SID = *sid*  
Se usa para volver a crear un inicio de sesión. Solo se aplica a inicios de sesión con autenticación de SQL Server, no a los de Windows. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. SID del inicio de sesión de SQL Server: un valor literal (**binary(16)**) de 16 bytes basado en un GUID. Por ejemplo, `SID = 0x14585E90117152449347750164BA00A7`. 
  
DEFAULT_DATABASE **=**_database_  
Especifica la base de datos predeterminada que debe asignarse al inicio de sesión. Si no se incluye esta opción, el valor predeterminado es master. 
  
DEFAULT_LANGUAGE **=**_language_  
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
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](https://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- El [modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md) del servidor debe coincidir con el tipo de inicio de sesión para permitir el acceso.
- Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="permissions"></a>Permisos  
- Solo los usuarios con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al rol fijo de servidor **securityadmin** pueden crear inicios de sesión. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles.
- Si se utiliza la opción **CREDENTIAL** , también será necesario el permiso **ALTER ANY CREDENTIAL** en el servidor. 
  
## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Server, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
 - Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
  
 - Cree un rol de servidor definido por el usuario mediante [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE**... **ADD MEMBER** para agregar el nuevo inicio de sesión al rol de servidor definido por el usuario. Para obtener más información, vea [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). 
  
 - Utilice **sp_addsrvrolemember** para agregar el inicio de sesión a un rol fijo de servidor. Para obtener más información, vea [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) y [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md). 
  
 - Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md). 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password-that-must-be-changed"></a>b. Crear un inicio de sesión con una contraseña que se debe cambiar
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
  
## <a name="see-also"></a>Consulte también  
- [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
- [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
- [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
- [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
- [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2016)|**_\* Servidor lógico de <br />SQL Database \*_**|[Instancia administrada de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[Almacenamiento de datos<br /> paralelos](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-logical-server"></a>Servidor lógico de Azure SQL Database
  
## <a name="syntax"></a>Sintaxis 
  
```
-- Syntax for Azure SQL Database  
CREATE LOGIN login_name  
 { WITH <option_list> }  
  
<option_list> ::=   
    PASSWORD = { 'password' }  
    [ , SID = sid ]  
```  

## <a name="arguments"></a>Argumentos  
*login_name*  
Especifica el nombre del inicio de sesión que se va a crear. El servidor lógico de Azure SQL Database solo admite los inicios de sesión SQL. 

PASSWORD **="** contraseña**"*  
Especifica la contraseña del inicio de sesión SQL que se está creando. Utilice una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la información de la contraseña almacenada se calcula con las funciones SHA-512 de la contraseña salada. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres de longitud y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 

SID = *sid*  
Se usa para volver a crear un inicio de sesión. Solo se aplica a inicios de sesión con autenticación de SQL Server, no a los de Windows. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. Para SQL Database, esto es un literal (**binary(32)**) de 32 bytes que consta de `0x01060000000000640000000000000000` más 16 bytes que representan un GUID. Por ejemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`. 
  
## <a name="remarks"></a>Notas  
- En las contraseñas se distingue entre mayúsculas y minúsculas.
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](https://support.microsoft.com/kb/918992).
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
  
 Para obtener más información sobre los inicios de sesión de SQL Database, vea [Administrar bases de datos e inicios de sesión en Microsoft Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins). 
 
## <a name="permissions"></a>Permisos

Solo pueden crear inicios de sesión el inicio de sesión de entidad de seguridad a nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos `loginmanager` en la base de datos maestra. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).<https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles>.

## <a name="logins"></a>Inicios de sesión
- Debe tener el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al rol fijo de servidor **securityadmin**. Solo la cuenta de Azure Active Directory (Azure AD) con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al permiso securityadmin pueden ejecutar este comando.
- Debe ser un miembro de Azure AD en el mismo directorio que se use para el servidor lógico de Azure SQL.
  
## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Database, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
- Para conectarse a una base de datos, cree un usuario de base de datos para el inicio de sesión en esa base de datos. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
- Para conceder permisos a un usuario en una base de datos, use la instrucción **ALTER SERVER ROLE**... **ADD MEMBER** para agregar al usuario a uno de los roles de base de datos integrados o a un rol personalizado, o bien conceda los permisos al usuario directamente mediante la instrucción [GRANT](../../t-sql/statements/grant-transact-sql.md). Para más información, vea [Roles no administradores](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles y la instrucción [GRANT](grant-transact-sql.md).
- Para conceder permisos de todo el servidor, cree un usuario de base de datos en la base de datos maestra y use la instrucción **ALTER SERVER ROLE**... **ADD MEMBER** para agregar al usuario a uno de los roles de servidor de administración. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) y [Roles de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).
- Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-from-a-sid"></a>b. Crear un inicio de sesión de un SID  
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
  
## <a name="see-also"></a>Consulte también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2016)|[Servidor lógico de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-current)|**_\* Instancia administrada de <br />SQL Database \*_**|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|[Almacenamiento de datos<br /> paralelos](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instancia administrada de Azure SQL Database

## <a name="syntax"></a>Sintaxis 
  
```sql
-- Syntax for Azure SQL Database Managed Instance
CREATE LOGIN login_name [FROM EXTERNAL PROVIDER] { WITH <option_list> [,..]}
  
<option_list> ::=
    PASSWORD = {'password'}
    | SID = sid
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language  
```  

> [!IMPORTANT]
> Los inicios de sesión de Azure AD para Instancia administrada de SQL Database están en **versión preliminar pública**. Esto se presentó con la sintaxis **FROM EXTERNAL PROVIDER**.

## <a name="arguments"></a>Argumentos
*login_name*  
Cuando se usa con la cláusula **FROM EXTERNAL PROVIDER**, el inicio de sesión especifica la entidad de seguridad de Azure Active Directory (AD), que es un usuario, un grupo o una aplicación de Azure AD. En caso contrario, el inicio de sesión representa el nombre del inicio de sesión SQL que se ha creado.

FROM EXTERNAL PROVIDER </br>
Especifica que el inicio de sesión es para la autenticación de Azure AD.

PASSWORD **=** '*password*'  
Especifica la contraseña del inicio de sesión SQL que se está creando. Utilice una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la información de la contraseña almacenada se calcula con las funciones SHA-512 de la contraseña salada. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres de longitud y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*.

SID **=** *sid*  
Se usa para volver a crear un inicio de sesión. Solo se aplica a los inicios de sesión con autenticación de SQL Server. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. Para SQL Database, esto es un literal (**binary(32)**) de 32 bytes que consta de `0x01060000000000640000000000000000` más 16 bytes que representan un GUID. Por ejemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`. 

## <a name="remarks"></a>Notas

- En las contraseñas se distingue entre mayúsculas y minúsculas.
- La nueva sintaxis se presentó para la creación de entidades de seguridad de nivel de servidor asignadas a cuentas de Azure AD (**FROM EXTERNAL PROVIDER**)
- Cuando se especifica **FROM EXTERNAL PROVIDER**:
    - login_name debe representar una cuenta de Azure AD (usuario, grupo o aplicación) existente que sea accesible en Azure AD mediante la Instancia administrada de Azure SQL actual.
    - No se puede usar la opción **PASSWORD**.
    - Actualmente, el primer inicio de sesión de Azure AD lo tiene que crear la cuenta de SQL Server estándar (que no sea de Azure AD) que sea `sysadmin` mediante la sintaxis anterior.
        - Al crear un inicio de sesión de Azure AD mediante un administrador de Azure AD para la Instancia administrada de SQL Database, se produce el error siguiente:</br>
        `Msg 15247, Level 16, State 1, Line 1
        User does not have permission to perform this action.`
        - Se trata de una limitación conocida de la **versión preliminar pública** y se corregirá en el futuro.
    - Una vez creado el primer inicio de sesión de Azure AD, este puede crear otros inicios de sesión de Azure AD una vez que se le hayan concedido los permisos necesarios.
- De forma predeterminada, cuando se omite la cláusula **FROM EXTERNAL PROVIDER**, se crea un inicio de sesión SQL convencional.
- Los inicios de sesión de Azure AD son visibles en sys.server_principals, con el valor de columna de tipo establecido en **E** y type_desc establecido en **EXTERNAL_LOGIN** para los inicios de sesión asignados a usuarios de Azure AD, o bien con el valor de tipo de columna establecido en **X** y el valor type_desc establecido en **EXTERNAL_GROUP** para los inicios de sesión asignados a grupos de Azure AD.
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](https://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor.
  
## <a name="logins-and-permissions"></a>Inicios de sesión y permisos

Solo pueden crear inicios de sesión el inicio de sesión de entidad de seguridad de nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros de los roles de base de datos `securityadmin` o `sysadmin` en la base de datos principal. Para más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).

De forma predeterminada, el permiso estándar que se concede a un inicio de sesión de Azure AD recién creado en la base de datos principal es el siguiente:
- **CONNECT SQL** y **VIEW ANY DATABASE**.

### <a name="sql-database-managed-instance-logins"></a>Inicios de sesión de Instancia administrada de SQL Database

- Debe tener el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia a uno de los roles fijos de servidor `securityadmin` o `sysadmin`. Solo la cuenta de Azure Active Directory (Azure AD) con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia a uno de estos roles puede ejecutar el comando de creación.
- Si el inicio de sesión es una entidad de seguridad de SQL, solo los inicios de sesión que formen parte del rol `sysadmin` pueden usar el comando create para crear inicios de sesión para una cuenta de Azure AD.
- Debe ser un miembro de Azure AD en el mismo directorio que se use para Instancia administrada de Azure SQL.

## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, se puede conectar a una Instancia administrada de SQL Database, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
- Para crear un usuario de Azure AD a partir de un inicio de sesión de Azure AD, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
- Para conceder permisos a un usuario en una base de datos, use la instrucción **ALTER SERVER ROLE**... **ADD MEMBER** para agregar al usuario a uno de los roles de base de datos integrados o a un rol personalizado, o bien conceda los permisos al usuario directamente mediante la instrucción [GRANT](../../t-sql/statements/grant-transact-sql.md). Para más información, vea [Roles no administradores](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles y la instrucción [GRANT](grant-transact-sql.md).
- Para conceder permisos de todo el servidor, cree un usuario de base de datos en la base de datos maestra y use la instrucción **ALTER SERVER ROLE**... **ADD MEMBER** para agregar al usuario a uno de los roles de servidor de administración. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) y [Roles de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).
    - Use el comando siguiente para agregar el rol `sysadmin` a un inicio de sesión de Azure AD: `ALTER SERVER ROLE sysadmin ADD MEMBER [AzureAD_Login_name]`
- Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md).

## <a name="limitations"></a>Limitaciones

- No se admite establecer un inicio de sesión de Azure AD asignado a un grupo de Azure AD como el propietario de la base de datos.
- Se admite la suplantación de entidades de seguridad de nivel de servidor de Azure AD con otras entidades de seguridad de Azure AD, como la cláusula [EXECUTE AS](execute-as-transact-sql.md).
- Solo las entidades de seguridad de nivel de servidor de SQL (inicios de sesión) que formen parte del rol `sysadmin` pueden ejecutar las operaciones siguientes destinadas a entidades de seguridad de Azure AD:
  - EXECUTE AS USER
  - EXECUTE AS LOGIN
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña.

 ```sql
 CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
 GO  
 ```

### <a name="b-creating-a-login-from-a-sid"></a>b. Crear un inicio de sesión de un SID
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

### <a name="c-creating-a-login-for-a-local-azure-ad-account"></a>C. Creación de un inicio de sesión para una cuenta de Azure AD local
 En el ejemplo siguiente se crea un inicio de sesión para la cuenta de Azure AD joe@myaad.onmicrosoft.com que existe en la instancia *myaad* de Azure AD.

```sql
CREATE LOGIN [joe@myaad.onmicrosoft.com] FROM EXTERNAL PROVIDER
GO
```

### <a name="d-creating-a-login-for-a-federated-azure-ad-account"></a>D. Creación de un inicio de sesión para una cuenta de Azure AD federada
 En el ejemplo siguiente se crea un inicio de sesión para una cuenta de Azure AD federada bob@contoso.com que existe en la instancia *contoso* de Azure AD. El usuario bob también puede ser un usuario invitado.

```sql
CREATE LOGIN [bob@contoso.com] FROM EXTERNAL PROVIDER
GO
```

### <a name="e-creating-a-login-for-an-azure-ad-group"></a>E. Creación de un inicio de sesión para un grupo de Azure AD
 En el ejemplo siguiente se crea un inicio de sesión para el grupo de Azure AD *mygroup* que existe en la instancia *myaad* de Azure AD.

```sql
CREATE LOGIN [mygroup] FROM EXTERNAL PROVIDER
GO
```

### <a name="f-creating-a-login-for-an-azure-ad-application"></a>F. Creación de un inicio de sesión para una aplicación de Azure AD
 En el ejemplo siguiente se crea un inicio de sesión para la aplicación de Azure AD *myapp* que existe en la instancia *myaad* de Azure AD.

```sql
CREATE LOGIN [myapp] FROM EXTERNAL PROVIDER
```

### <a name="g-check-newly-added-logins"></a>G. Comprobación de los inicios de sesión recién agregados
 Para comprobar el inicio de sesión recién agregado, ejecute el siguiente comando de T-SQL:

```sql
SELECT *   
FROM sys.server_principals;
GO
```
  
## <a name="see-also"></a>Consulte también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  


  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2016)|[Servidor lógico de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-current)|[Instancia administrada de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-mi-current)|**_\* SQL Data<br />Warehouse \*_**|[Almacenamiento de datos<br /> paralelos](create-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-data-warehouse"></a>Almacenamiento de datos SQL de Azure
  
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
Especifica la contraseña del inicio de sesión SQL que se está creando. Utilice una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la información de la contraseña almacenada se calcula con las funciones SHA-512 de la contraseña salada. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres de longitud y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 

 SID = *sid*  
 Se usa para volver a crear un inicio de sesión. Solo se aplica a inicios de sesión con autenticación de SQL Server, no a los de Windows. Especifica el SID del nuevo inicio de sesión con autenticación de SQL Server. Si no se usa esta opción, SQL Server asigna un SID de manera automática. La estructura de SID depende de la versión de SQL Server. Para SQL Data Warehouse, esto es un literal (**binary(32)**) de 32 bytes que consta de `0x01060000000000640000000000000000` más 16 bytes que representan un GUID. Por ejemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`. 
  
## <a name="remarks"></a>Notas  
- En las contraseñas se distingue entre mayúsculas y minúsculas.
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](https://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- El [modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md) del servidor debe coincidir con el tipo de inicio de sesión para permitir el acceso.
    - Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).
  
## <a name="logins"></a>Inicios de sesión

La instrucción **CREATE LOGIN** debe ser la única de un lote. 
  
En algunos métodos de conexión con SQL Data Warehouse, como **sqlcmd**, debe anexar el nombre del servidor de SQL Data Warehouse al nombre de inicio de sesión en la cadena de conexión mediante la notación *\<inicio_de_sesión>*@*\<servidor>*. Por ejemplo, si el inicio de sesión es `login1` y el nombre completo del servidor de SQL Data Warehouse es `servername.database.windows.net`, el parámetro *nombre_de_usuario* de la cadena de conexión debe ser `login1@servername`. Dado que la longitud total del parámetro *username* es de 128 caracteres, *login_name* se limita a 127 caracteres menos la longitud del nombre del servidor. En el ejemplo, `login_name` solo puede tener 117 caracteres porque `servername` es de 10 caracteres. 
  
En SQL Data Warehouse, debe estar conectado a la base de datos maestra para crear un inicio de sesión. 
  
 Las reglas de SQL Server permiten crear un inicio de sesión con autenticación de SQL Server con el formato \<nombreDeInicioDeSesión>@\<nombreDeServidor>. Si el servidor de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] es **myazureserver** y el inicio de sesión es **myemail@live.com**, debe proporcionar un inicio de sesión como **myemail@live.com@myazureserver**. 
  
En SQL Data Warehouse, los datos de inicio de sesión necesarios para autenticar una conexión y las reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza regularmente. Para forzar una actualización de la caché de autenticación y garantizar que una base de datos tenga la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md). 
  
 Para obtener más información sobre los inicios de sesión de Azure SQL Data Warehouse, vea [Administrar bases de datos e inicios de sesión en Microsoft Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins). 
 
## <a name="permissions"></a>Permisos

Solo pueden crear inicios de sesión el inicio de sesión de entidad de seguridad a nivel de servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos `loginmanager` en la base de datos maestra. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).<https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles>.

## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Data Warehouse, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
- Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md).
- Para conceder permisos a un usuario en una base de datos, use la instrucción **ALTER SERVER ROLE**... **ADD MEMBER** para agregar al usuario a uno de los roles de base de datos integrados o a un rol personalizado, o bien conceda los permisos al usuario directamente mediante la instrucción [GRANT](grant-transact-sql.md). Para más información, vea [Roles no administradores](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#non-administrator-users), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles y la instrucción [GRANT](grant-transact-sql.md).
- Para conceder permisos de todo el servidor, cree un usuario de base de datos en la base de datos maestra y use la instrucción **ALTER SERVER ROLE**... **ADD MEMBER** para agregar al usuario a uno de los roles de servidor de administración. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles), [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) y [Roles de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles).

- Use la instrucción de **GRANT**, para conceder permisos de servidor al nuevo inicio de sesión o un rol que contiene el inicio de sesión. Para obtener más información, vea [GRANT](../../t-sql/statements/grant-transact-sql.md). 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. 
  
```sql  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  

### <a name="b-creating-a-login-from-a-sid"></a>b. Crear un inicio de sesión de un SID  
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
  
## <a name="see-also"></a>Consulte también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> [!div class="mx-tdCol2BreakAll"]
> ||||||
> |-|-|-|-|-|
> |[SQL Server](create-login-transact-sql.md?view=sql-server-2016)|[Servidor lógico de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-current)|[Instancia administrada de <br />SQL Database](create-login-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-login-transact-sql.md?view=azure-sqldw-latest)|**_\* Almacenamiento de datos<br /> paralelos \*_**

&nbsp;

## <a name="parallel-data-warehouse"></a>Almacenamiento de datos paralelos

  
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
Especifica el nombre del inicio de sesión que se va a crear. Hay cuatro tipos de inicios de sesión: inicios de sesión de SQL Server, de Windows, asignados a certificados y asignados a claves asimétricas. Cuando crea inicios de sesión que se asignan desde una cuenta de dominio de Windows, debe utilizar el nombre de inicio de sesión de usuario anterior a Windows 2000 con el formato[\<domainName>\\<login_name>]. No puede utilizar un UPN con el formato login_name@DomainName. Vea el ejemplo D más adelante en este artículo. Los inicios de sesión con autenticación son del tipo **sysname**, deben seguir las reglas de los [Identificadores](../../relational-databases/databases/database-identifiers.md) y no pueden contener "**\\**". Los inicios de sesión de Windows pueden contener un carácter '**\\**”. Los inicios de sesión basados en usuarios de Active Directory se limitan a nombres de menos de 21 caracteres. 

PASSWORD **="**_contraseña_" Solo se aplica a inicios de sesión de SQL Server. Especifica la contraseña del inicio de sesión que se está creando. Utilice una contraseña segura. Para obtener más información, vea [Contraseñas seguras](../../relational-databases/security/strong-passwords.md) y [Directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de SQL Server 2012 (11.x), la información de contraseña almacenada se calcula con SHA-512 de la contraseña cifrada con sal. 
  
En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres de longitud y no pueden superar los 128 caracteres. Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples ni *login_name*. 
  
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
  
- Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](https://support.microsoft.com/kb/918992).
- Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor. 
- Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).

## <a name="permissions"></a>Permisos  
Solo los usuarios con el permiso **ALTER ANY LOGIN** en el servidor o la pertenencia al rol fijo de servidor **securityadmin** pueden crear inicios de sesión. Para obtener más información, vea [Roles de nivel de servidor](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#groups-and-roles) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md).<https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins#additional-server-level-administrative-roles>.
  
## <a name="after-creating-a-login"></a>Después de crear un inicio de sesión  
Después de crear un inicio de sesión, el inicio de sesión se puede conectar a SQL Data Warehouse, pero solo tiene los permisos concedidos al rol **public**. Considere la posibilidad de realizar algunas de las actividades siguientes. 
  
 - Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER](../../t-sql/statements/create-user-transact-sql.md). 
  
 - Cree un rol de servidor definido por el usuario mediante [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE**... **ADD MEMBER** para agregar el nuevo inicio de sesión al rol de servidor definido por el usuario. Para obtener más información, vea [CREATE SERVER ROLE](../../t-sql/statements/create-server-role-transact-sql.md) y [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md). 
  
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
  
## <a name="see-also"></a>Consulte también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
---  

::: moniker-end
