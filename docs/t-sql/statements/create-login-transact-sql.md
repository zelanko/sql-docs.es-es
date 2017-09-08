---
title: "CREAR el inicio de sesión (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f64c2f34c7e0c2d8c768b5a846465a65ed51082d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea un inicio de sesión del [!INCLUDE[ssDE](../../includes/ssde-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE LOGIN login_name  
 { WITH <option_list3> }  
  
<option_list3> ::=   
    PASSWORD = { 'password' }  
    [ SID = sid ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  
  
## <a name="arguments"></a>Argumentos  
 *login_name*  
 Especifica el nombre del inicio de sesión que se va a crear. Hay cuatro tipos de inicio de sesión: de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], de Windows, asignado a un certificado y asignado a una clave asimétrica. Al crear los inicios de sesión que se asignan desde una cuenta de dominio de Windows, debe usar el nombre de inicio de sesión de usuario anterior a Windows 2000 en el formato [\<domainName >\\< login_name >]. No se puede utilizar un UPN con el formato login_name@DomainName. Vea el ejemplo D más adelante en este tema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]los inicios de sesión de autenticación son tipo **sysname** y debe cumplir las reglas de [identificadores](http://msdn.microsoft.com/library/ms175874.aspx) y no puede contener un '**\\**'. Los inicios de sesión de Windows pueden contener un carácter '**\\**”. Inicios de sesión basados en usuarios de Active Directory, están limitados a nombres de menos de 21 caracteres.  
  
 CONTRASEÑA **='***contraseña***'**  
 Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión. Especifica la contraseña del inicio de sesión que se está creando. Debe utilizar siempre una contraseña segura. Para obtener más información, consulte [Strong Passwords](../../relational-databases/security/strong-passwords.md) y [directiva de contraseñas](../../relational-databases/security/password-policy.md). A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]almacenadas información de contraseña se calcula con SHA-512 de la contraseña con sal.  
  
 En las contraseñas se distingue entre mayúsculas y minúsculas. Las contraseñas siempre deben ser de al menos 8 caracteres y no pueden superar los 128 caracteres.  Las contraseñas pueden incluir a-z, A-Z, 0-9 y la mayoría de los caracteres no alfanuméricos. Las contraseñas no pueden contener comillas simples, o la *login_name*.  
  
 CONTRASEÑA  **=**  *hashed_password*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a la palabra clave HASHED. Especifica el valor con hash de la contraseña para el inicio de sesión que se está creando.  
  
 HASHED  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión. Especifica que la contraseña especificada después del argumento PASSWORD ya tiene aplicado el algoritmo hash. Si no se selecciona esta opción, se aplicará el algoritmo hash a la cadena especificada como contraseña antes de almacenarla en la base de datos. Esta opción solo se debería utilizar para migrar las bases de datos de un servidor a otro. No utilice la opción HASHED para crear nuevos inicios de sesión. La opción HASHED no se puede utilizar con los valores hash creados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7 o anterior.  
  
 MUST_CHANGE  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión. Si se incluye esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pide al usuario la contraseña nueva la primera vez que se utilice el inicio de sesión nuevo.  
  
 CREDENCIAL  **=**  *credential_name*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Nombre de una credencial que debe asignarse al nuevo inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La credencial debe existir en la base de datos. Actualmente esta opción solo vincula la credencial a un inicio de sesión. No se puede asignar una credencial para el inicio de sesión de administrador del sistema (sa).  
  
 SID = *sid*  
 Se usa para volver a crear un inicio de sesión. Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión de autenticación, no conexiones de autenticación de Windows. Especifica el SID del nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de autenticación. Si no se usa esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna automáticamente un SID. La estructura de SID depende el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SID del inicio de sesión: un 16 bytes (**binary (16)**) valor literal según un GUID. Por ejemplo, `SID = 0x14585E90117152449347750164BA00A7`.  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)]SID del inicio de sesión: una estructura de SID válida para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Normalmente se trata de un byte 32 (**binary(32)**) literal formada por `0x01060000000000640000000000000000` más 16 bytes que representa un GUID. Por ejemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.  
  
DEFAULT_DATABASE  **=**  *base de datos*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la base de datos predeterminada que debe asignarse al inicio de sesión. Si no se incluye esta opción, el valor predeterminado es master.  
  
DEFAULT_LANGUAGE  **=**  *idioma*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el idioma predeterminado que debe asignarse al inicio de sesión. Si no se incluye esta opción, el idioma predeterminado es el del servidor. Si el idioma predeterminado del servidor se cambia más tarde, el del inicio de sesión se mantiene igual.  
  
CHECK_EXPIRATION  **=**  {ON | **OFF** }  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión. Especifica si debe aplicarse la directiva de caducidad de contraseñas en este inicio de sesión. El valor predeterminado es OFF.  
  
CHECK_POLICY  **=**  { **ON** | {OFF}  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión. Especifica que se deben aplicar las directivas de contraseñas de Windows en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este inicio de sesión. El valor predeterminado es ON.  
  
 Si la directiva de Windows requiere contraseñas seguras, las contraseñas deben tener al menos tres de las cuatro siguientes características:  
  
-   Un carácter en mayúscula (A-Z).  
-   Un carácter en minúsculas (a-z).  
-   Un dígito (0-9).  
-   Uno de los caracteres no alfanuméricos, como un espacio, _, @, *, ^, %, !, $, # o &.  
  
WINDOWS  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que el inicio de sesión se asigna a un inicio de sesión de Windows.  
  
CERTIFICADO *certname*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el nombre de un certificado al que asociar este inicio de sesión. Este certificado debe existir en la base de datos maestra.  
  
CLAVE ASIMÉTRICA *asym_key_name*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el nombre de una clave asimétrica a la que asociar este inicio de sesión. Esta clave debe existir en la base de datos maestra.  
  
## <a name="remarks"></a>Comentarios  
 En las contraseñas se distingue entre mayúsculas y minúsculas.  
  
 La aplicación previa del algoritmo hash a las contraseñas solo se admite en la creación de inicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si se especifica MUST_CHANGE, CHECK_EXPIRATION y CHECK_POLICY, deben establecerse en ON. Si no es así, la instrucción producirá un error.  
  
 No se admite la combinación de CHECK_POLICY = OFF y CHECK_EXPIRATION = ON.  
  
 Cuando CHECK_POLICY se establece en OFF, *lockout_time* se restablece y CHECK_EXPIRATION se establece en OFF.  
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION y CHECK_POLICY solo se aplican en [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] y versiones posteriores. Para obtener más información, vea [Password Policy](../../relational-databases/security/password-policy.md).  
  
 Los inicios de sesión creados con certificados o claves asimétricas solo se usan para la firma del código. No se pueden utilizar para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Solo puede crear un inicio de sesión desde un certificado o clave asimétrica cuando este certificado o clave asimétrica ya exista en la base de datos maestra.  
  
 Para obtener un script para transferir inicios de sesión, vea [Cómo transferir los inicios de sesión y las contraseñas entre instancias de SQL Server 2005 y SQL Server 2008](http://support.microsoft.com/kb/918992).  
  
 Al crear un inicio de sesión automáticamente se habilita el nuevo inicio de sesión y se concede al mismo el permiso de **CONNECT SQL** de nivel servidor.  
  
 Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-and-includesssdwincludessssdw-mdmd-logins"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los inicios de sesión  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], **CREATE LOGIN** debe ser la única instrucción en un lote.  
  
 En algunos métodos de conexión a [!INCLUDE[ssSDS](../../includes/sssds-md.md)], como **sqlcmd**, debe anexar el [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nombre del servidor para el nombre de inicio de sesión en la cadena de conexión mediante el uso de la  *\<inicio de sesión >* @  *\<server >* notación. Por ejemplo, si el inicio de sesión `login1` y el nombre completo de la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor es `servername.database.windows.net`, *nombre de usuario* parámetro de la cadena de conexión debe ser `login1@servername`. Dado que la longitud total de la *nombre de usuario* parámetro es de 128 caracteres, *login_name* está limitada a 127 caracteres menos la longitud del nombre del servidor. En el ejemplo, `login_name` solo puede tener 117 caracteres porque `servername` es de 10 caracteres.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] debe estar conectado a la base de datos maestra para crear un inicio de sesión.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]las reglas permiten crear un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de autenticación en el formato \<loginname > @\<nombreDeServidor >. Si su [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor es **myazureserver** y su inicio de sesión es  **myemail@live.com** , debe proporcionar el inicio de sesión como  **myemail@live.com @myazureserver**  .  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], datos de inicio de sesión necesitan para autenticar una conexión y las reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza periódicamente. Para forzar una actualización de la caché de autenticación y asegúrese de que una base de datos tiene la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
 Para obtener más información acerca de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] inicios de sesión, vea [administrar bases de datos e inicios de sesión en Windows Azure SQL Database](http://msdn.microsoft.com/library/ee336235.aspx).  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], requiere **ALTER ANY LOGIN** permiso en el servidor o la pertenencia a la **securityadmin** rol fijo de servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], solo pueden crear nuevos inicios de sesión el inicio de sesión principal de nivel servidor (creado por el proceso de aprovisionamiento) o los miembros del rol de base de datos de `loginmanager` en la base de datos maestra.  
  
 Si se utiliza la opción **CREDENTIAL** , también será necesario el permiso **ALTER ANY CREDENTIAL** en el servidor.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Después de crear un inicio de sesión, el inicio de sesión puede conectarse a la [!INCLUDE[ssDE](../../includes/ssde-md.md)] o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] pero solo tiene los permisos concedidos a la **público** rol. Considere realizar algunas de las actividades siguientes.  
  
-   Para conectarse a una base de datos, cree una para el inicio de sesión. Para obtener más información, vea [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
-   Crear un rol de servidor definido por el usuario mediante [CREATE SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** ... **Agregar miembro** para agregar el nuevo inicio de sesión para el rol de servidor definido por el usuario. Para obtener más información, vea [CREATE SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-server-role-transact-sql.md) y [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
-   Use **sp_addsrvrolemember** para agregar el inicio de sesión a un rol fijo de servidor. Para obtener más información, consulte [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) y [sp_addsrvrolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
-   Use la **GRANT** instrucción para conceder permisos de nivel de servidor para el nuevo inicio de sesión o a una función que contiene el inicio de sesión. Para obtener más información, vea [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña.  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password"></a>B. Crear un inicio de sesión con una contraseña  
 El ejemplo siguiente crea un inicio de sesión para un usuario determinado y le asigna una contraseña. La opción `MUST_CHANGE` exige a los usuarios que cambien la contraseña la primera vez que se conecten al servidor.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' MUST_CHANGE;  
GO  
```  
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. Crear un inicio de sesión asignado a una credencial  
 El ejemplo siguiente crea el inicio de sesión para un usuario determinado, utilizando el de usuario. Este inicio de sesión se asigna a la credencial.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. Crear un inicio de sesión desde un certificado  
 En el ejemplo siguiente se crea el inicio de sesión para un usuario determinado de un certificado de master.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
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
  
```  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. Crear un inicio de sesión de un SID  
 En el ejemplo siguiente se crea primero un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de autenticación y determina el SID del inicio de sesión.  
  
```  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 La consulta devuelve 0x241C11948AEEB749B0D22646DB1A19F2 como el SID. La consulta devolverá un valor diferente. Las siguientes instrucciones eliminan el inicio de sesión y luego vuelven a crear el inicio de sesión. Use el SID de la consulta anterior.  
  
```  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. Crear un inicio de sesión de autenticación de SQL Server con una contraseña  
 En el ejemplo siguiente se crea el inicio de sesión `Mary7` con contraseña `A2c3456`.  
  
```tsql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. Uso de opciones  
 En el ejemplo siguiente se crea el inicio de sesión `Mary8` con contraseña algunos de los argumentos opcionales.  
  
```  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. Crear un inicio de sesión desde una cuenta de dominio de Windows  
 En el ejemplo siguiente se crea un inicio de sesión desde una cuenta de dominio de Windows denominada `Mary` en el `Contoso` dominio.  
  
```  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [QUITAR el inicio de sesión &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  

