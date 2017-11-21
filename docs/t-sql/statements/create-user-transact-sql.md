---
title: Crear usuario (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITHOUT_LOGIN_TSQL
- CREATE_USER_TSQL
- SQL13.SWB.DATABASEUSER.OWNEDSCHEMAS.F1
- WITHOUT LOGIN
- CREATE USER
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- adding users
- WITHOUT LOGIN [SQL Server]
- CREATE USER statement
- database user additions [SQL Server]
- USER WITHOUT LOGIN [SQL Server]
- users [SQL Server], adding
- users [SQL Server]
ms.assetid: 01de7476-4b25-4d58-85b7-1118fe64aa80
caps.latest.revision: 111
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47004dfe9ec810fec68a63849755021690f98fdb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-user-transact-sql"></a>CREATE USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Agrega un usuario a la base de datos actual. Los tipos de once de usuario se enumeran a continuación con un ejemplo de la sintaxis más sencilla:  
  
**Los usuarios basados en inicios de sesión en master** trata el tipo más común del usuario.  
  
-   Usuario basado en un inicio de sesión basada en una cuenta de Active Directory de Windows. `CREATE USER [Contoso\Fritz];`     
-   Usuario basado en un inicio de sesión basado en un grupo de Windows. `CREATE USER [Contoso\Sales];`   
-   Usuario basado en un inicio de sesión mediante autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `CREATE USER Mary;`  
  
**Los usuarios que se autentican en la base de datos** recomendado para ayudar a que la base de datos sea más portable.  
 Siempre se permite en [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. Solo se permiten en una base de datos independiente en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
-   Usuario basado en un usuario de Windows sin inicio de sesión. `CREATE USER [Contoso\Fritz];`    
-   Usuario basado en un grupo de Windows sin inicio de sesión. `CREATE USER [Contoso\Sales];`  
-   Usuario de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] o [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] según un usuario de Azure Active Directory. `CREATE USER [Contoso\Fritz] FROM EXTERNAL PROVIDER;`     

-   Usuario de base de datos independiente con contraseña. (No está disponible en [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].)`CREATE USER Mary WITH PASSWORD = '********';`   
  
**Usuarios en función de las entidades de seguridad de Windows que se conectan a través de inicios de sesión de grupo de Windows**  
  
-   Usuario basado en un usuario de Windows sin inicio de sesión, pero que se puede conectar a [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante la pertenencia a un grupo de Windows. `CREATE USER [Contoso\Fritz];`  
  
-   Usuario basado en un grupo de Windows sin inicio de sesión, pero que se puede conectar a [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante la pertenencia a un grupo distinto de Windows. `CREATE USER [Contoso\Fritz];`  
  
**Los usuarios que no se pueden autenticar** estos usuarios no pueden iniciar sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
-   Usuario sin inicio de sesión. No puede iniciar sesión, pero se le pueden conceder permisos. `CREATE USER CustomApp WITHOUT LOGIN;`    
-   Usuario basado en un certificado. No puede iniciar sesión, pero se le pueden conceder permisos y puede firmar módulos. `CREATE USER TestProcess FOR CERTIFICATE CarnationProduction50;`  
-   Usuario basado en una clave asimétrica. No puede iniciar sesión, pero se le pueden conceder permisos y puede firmar módulos. `CREATE User TestProcess FROM ASYMMETRIC KEY PacificSales09;`   
 
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Syntax Users based on logins in master  
CREATE USER user_name   
    [   
        { FOR | FROM } LOGIN login_name   
    ]  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that authenticate at the database  
CREATE USER   
    {  
      windows_principal [ WITH <options_list> [ ,... ] ]  
  
    | user_name WITH PASSWORD = 'password' [ , <options_list> [ ,... ]   
    | Azure_Active_Directory_principal FROM EXTERNAL PROVIDER   
    }  
  
 [ ; ]  
  
--Users based on Windows principals that connect through Windows group logins  
CREATE USER   
    {   
          windows_principal [ { FOR | FROM } LOGIN windows_principal ]  
        | user_name { FOR | FROM } LOGIN windows_principal  
}  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that cannot authenticate   
CREATE USER user_name   
    {  
         WITHOUT LOGIN [ WITH <limited_options_list> [ ,... ] ]  
       | { FOR | FROM } CERTIFICATE cert_name   
       | { FOR | FROM } ASYMMETRIC KEY asym_key_name   
    }  
 [ ; ]  
  
<options_list> ::=  
      DEFAULT_SCHEMA = schema_name  
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }  
    | SID = sid   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name ]   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
-- SQL Database syntax when connected to a federation member  
CREATE USER user_name  
[;]  
```  

```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM } { LOGIN login_name }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]

CREATE USER Azure_Active_Directory_principal FROM EXTERNAL PROVIDER  
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]
``` 
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM }  
      {   
        LOGIN login_name   
      }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *user_name*  
 Especifica el nombre por el que se identifica al usuario en esta base de datos. *user_name* es un **sysname**. Puede tener una longitud máxima de 128 caracteres. Cuando se crea un usuario basado en una entidad de seguridad de Windows, el nombre de esta entidad se convierte en el nombre de usuario a menos que se especifique otro nombre de usuario.  
  
 Inicio de sesión *login_name*  
 Especifica el inicio de sesión para el que se crea el usuario de base de datos. *login_name* debe ser un inicio de sesión válido en el servidor. Puede ser un inicio de sesión basado en una entidad de seguridad de Windows (usuario o grupo) o un inicio de sesión con autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando este inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se introduce en la base de datos adquiere el nombre y el identificador del usuario de la base de datos que se está creando. Al crear un inicio de sesión se asigna desde una entidad de seguridad de Windows, use el formato **[***\<domainName >*  **\\**   *\<loginName >***]**. Para obtener ejemplos, vea [resumen de la sintaxis](#SyntaxSummary).  
  
 Si la instrucción CREATE USER es la única instrucción en un lote SQL, SQL Database de Microsoft Azure admite la cláusula WITH LOGIN. Si la instrucción CREATE USER no es la única instrucción en un lote SQL ni se ejecuta en SQL dinámico, la cláusula WITH LOGIN no se admite.  
  
 CON DEFAULT_SCHEMA = *schema_name*  
 Especifica el primer esquema donde buscará el servidor cuando resuelva los nombres de objetos de este usuario de base de datos.  
  
 '*windows_principal*'  
 Especifica la entidad de seguridad de Windows para la que se crea el usuario de base de datos. El *windows_principal* puede ser un usuario de Windows o un grupo de Windows. Se creará el usuario incluso si la *windows_principal* no tiene un inicio de sesión. Cuando se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si la *windows_principal* no tiene un inicio de sesión, las ventanas de entidad de seguridad debe autenticar en el [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante la pertenencia a un grupo de Windows que tiene un inicio de sesión o la cadena de conexión debe Especifique la base de datos independiente como el catálogo inicial. Al crear un usuario de una entidad de seguridad de Windows, use el formato **[***\<domainName >*  **\\**   *\< loginName >***]**. Para obtener ejemplos, vea [resumen de la sintaxis](#SyntaxSummary). Los usuarios en función de los usuarios de Active Directory, están limitados a nombres de menos de 21 caracteres.    
  
 '*Azure_Active_Directory_principal*'  
 **Se aplica a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)], [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)].  
  
 Especifica la entidad de seguridad de Azure Active Directory para el que se está creando el usuario de base de datos. El *Azure_Active_Directory_principal* puede ser un usuario de Azure Active Directory o a un grupo de Active Directory de Azure. (Los usuarios de azure Active Directory no pueden tener inicios de sesión de autenticación de Windows en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]; solo los usuarios de base de datos.) La cadena de conexión debe especificar la base de datos independiente como el catálogo inicial. 

 Para los usuarios, utilice el alias completo de su dominio principal.   
 
-   `CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;`  
  
-   `CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;`

 Para los grupos de seguridad, use la *nombre para mostrar* del grupo de seguridad. Para el *enfermeras* grupo de seguridad, utilizaría:  
  
-   `CREATE USER [Nurses] FROM EXTERNAL PROVIDER;`  
  
 Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication).  
  
CON contraseña = '*contraseña*'  
 **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Solo se puede usar en una base de datos independiente. Especifica la contraseña del usuario que se está creando. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]almacenadas información de contraseña se calcula con SHA-512 de la contraseña con sal.  
  
WITHOUT LOGIN  
 Especifica que el usuario no se debe asignar a ningún inicio de sesión existente.  
  
CERTIFICADO *cert_name*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica el certificado del usuario de la base de datos que se crea.  
  
CLAVE ASIMÉTRICA *asym_key_name*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica la clave asimétrica del usuario de la base de datos que se crea.  
  
DEFAULT_LANGUAGE = *{NONE | \<lcid > | \<nombreidioma > | \<aliasidioma >}*  
 **Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica el idioma predeterminado del nuevo usuario. Si se especifica un idioma predeterminado para el usuario y el idioma de la base de datos se cambia posteriormente, el idioma predeterminado de los usuarios se mantiene como se especificó. Si no se especifica ningún idioma predeterminado, el idioma predeterminado del usuario será el idioma predeterminado de la base de datos. Si no se especificó ningún idioma predeterminado para el usuario y el idioma predeterminado de la base de datos se cambia posteriormente, el idioma predeterminado del usuario se cambiará al nuevo idioma predeterminado de la base de datos.  
  
> [!IMPORTANT]  
>  *DEFAULT_LANGUAGE* solo se usa para un usuario de base de datos independiente.  
  
SID = *sid*  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a los usuarios con las contraseñas (autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) en una base de datos independiente. Especifica el SID de la base de datos. Si esta opción no se selecciona, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna automáticamente un SID. Utilice el parámetro SID para crear usuarios en varias bases de datos que tienen la misma identidad (SID). Esto es útil para crear usuarios de varias bases de datos para prepararse para siempre en conmutación por error. Para determinar al SID de un usuario, consulte sys.database_principals.  
  
ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ON | **OFF** ]]  
 **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Suprime las comprobaciones de metadatos criptográficos en el servidor en operaciones de copia masiva. Esto permite al usuario copiar los datos de forma masiva entre tablas o bases de datos, sin descifrar los datos. El valor predeterminado es OFF.  
  
> [!WARNING]  
>  Si esta opción no se utiliza adecuadamente, pueden dañarse los datos. Para obtener más información, consulte [migrar información confidencial protegida mediante Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
## <a name="remarks"></a>Comentarios  
 Si se omite FOR LOGIN, el nuevo usuario de base de datos se asignará al inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el mismo nombre.  
  
 El esquema predeterminado será el primer esquema donde buscará el servidor cuando resuelva los nombres de objetos de este usuario de base de datos. A menos que se especifique lo contrario, el esquema predeterminado será el propietario de los objetos creados por este usuario de base de datos.  
  
 Si el usuario tiene un esquema predeterminado, se utilizará dicho esquema. Si el usuario no tiene un esquema predeterminado pero es miembro de un grupo con un esquema predeterminado, se utilizará el esquema predeterminado del grupo. Si el usuario no tiene un esquema predeterminado y es miembro de varios grupos, el esquema predeterminado para el usuario será el del grupo de Windows con el principal_id mínimo y un esquema predeterminado establecido explícitamente. No es posible seleccionar explícitamente uno de los esquemas predeterminados disponibles como esquema preferido. Si no se puede determinar ningún esquema predeterminado para un usuario, el **dbo** se utilizará el esquema.  
  
 DEFAULT_SCHEMA puede establecerse antes de crear el esquema que lo señala.  
  
 No se puede especificar DEFAULT_SCHEMA cuando se está creando un usuario asignado a un certificado o una clave asimétrica.  
  
 El valor de DEFAULT_SCHEMA se omite si el usuario es un miembro del rol fijo de servidor sysadmin. Todos los miembros del rol fijo de servidor sysadmin tienen un esquema predeterminado de `dbo`.  
  
 La cláusula WITHOUT LOGIN crea un usuario que no se asigna a ningún inicio de sesión de SQL Server. Este usuario puede conectarse a otras bases de datos como guest. Se pueden asignar permisos a este usuario sin inicio de sesión y cuando cambie el contexto de seguridad a un usuario sin inicio de sesión, el usuario original recibe el permiso del usuario sin inicio de sesión. Vea el ejemplo [D. crear y utilizar un usuario sin inicio de sesión](#withoutLogin).  
  
 Solo los usuarios que están asignados a entidades de seguridad de Windows pueden contener el carácter de barra diagonal inversa (**\\**).  
  
 No se puede utilizar CREATE USER para crear un usuario guest porque el usuario guest ya existe en cada base de datos. Puede habilitar el usuario guest concediéndole el permiso CONNECT como se muestra a continuación:  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
 Información acerca de los usuarios de base de datos está visible en el [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) vista de catálogo.  
  
##  <a name="SyntaxSummary"></a>Resumen de la sintaxis  
 **Usuarios basados en inicios de sesión en master**  
  
 En la siguiente lista se muestra la posible sintaxis de los usuarios basados en inicios de sesión. No se citan las opciones de esquema predeterminadas.  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN`  
  
**Usuarios que se autentican en la base de datos**  
  
 En la siguiente lista se muestra la posible sintaxis de los usuarios que solo se puede usar en una base de datos independiente. Los usuarios creados no esté relacionado con los inicios de sesión en la **maestro** base de datos. No se muestran las opciones predeterminadas de esquema ni de idioma.  
  
> [!IMPORTANT]  
>  Esta sintaxis concede acceso a los usuarios a la base de datos, así como nuevo acceso a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'`  
  
**Usuarios en función de las entidades de seguridad de Windows sin inicios de sesión en master**  
  
 En la lista siguiente muestra la posible sintaxis para los usuarios que tienen acceso a la [!INCLUDE[ssDE](../../includes/ssde-md.md)] a través de una ventana de grupo pero no tiene un inicio de sesión **principal**. Esta sintaxis se puede usar en todos los tipos de bases de datos. No se muestran las opciones predeterminadas de esquema ni de idioma.  
  
 Esta sintaxis es similar a la de los usuarios basados en inicios de sesión en la base de datos maestra, pero esta categoría no dispone de inicio de sesión en dicha base de datos. El usuario debe tener acceso a [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante un inicio de sesión de grupo de Windows.  
  
 Esta sintaxis es similar a la de los usuarios de bases de datos independientes basados en las entidades de seguridad de Windows, pero esta categoría de usuario no obtiene nuevo acceso a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
  
**Usuarios que no se pueden autenticar**  
  
 En la siguiente lista se muestra la posible sintaxis para los usuarios que no pueden iniciar sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   `CREATE USER RIGHTSHOLDER WITHOUT LOGIN`  
-   `CREATE USER CERTUSER FOR CERTIFICATE SpecialCert`  
-   `CREATE USER CERTUSER FROM CERTIFICATE SpecialCert`  
-   `CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey`  
-   `CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey`  
  
## <a name="security"></a>Seguridad  
 Si se crea un usuario, se le concede acceso a una base de datos, pero no se le concede ningún acceso automáticamente a los objetos de una base de datos. Después de crear un usuario, las acciones habituales son agregar a los usuarios a los roles de base de datos con permiso para acceder a los objetos de la base de datos o conceder permisos de objeto al usuario. Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
### <a name="special-considerations-for-contained-databases"></a>Consideraciones especiales para bases de datos independientes  
 Al conectarse a una base de datos independiente, si el usuario no tiene un inicio de sesión la **maestro** base de datos, la cadena de conexión debe incluir el nombre de la base de datos independiente como el catálogo inicial. El parámetro de catálogo inicial siempre es necesario para un usuario de base de datos independiente con contraseña.  
  
 En una base de datos independiente, la creación de usuarios ayuda a separar la base de datos de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que la base de datos se pueda mover fácilmente a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [las bases de datos](../../relational-databases/databases/contained-databases.md) y [base de datos de usuarios independiente: hacer que la base de datos portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md). Para cambiar un usuario de base de datos de un usuario basándose en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión de autenticación a un usuario de base de datos independiente con contraseña, consulte [sp_migrate_user_to_contained &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).  
  
 En una base de datos independiente, los usuarios no deben tener inicios de sesión en la **maestro** base de datos. Los administradores del [!INCLUDE[ssDE](../../includes/ssde-md.md)] deben comprender que el acceso a una base de datos independiente se puede conceder en el nivel de base de datos, en vez de en el nivel de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para más información, consulte [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
 Al usar los usuarios de la base de datos independiente de [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], configure el acceso con una regla de firewall de nivel de base de datos en lugar de una regla de firewall de nivel de servidor. Para obtener más información, consulte [sp_set_database_firewall_rule &#40; Base de datos SQL Azure &#41; ](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md).
 
Para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] usuarios de base de datos independiente, SSMS puede admitir la autenticación multifactor. Para más información, consulte [Compatibilidad de SSMS con Azure AD MFA con SQL Database y SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/).  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY USER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-database-user-based-on-a-sql-server-login"></a>A. Crear un usuario de base de datos basado en un inicio de sesión de SQL Server  
 En el siguiente ejemplo, primero se crea un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominado `AbolrousHazem` y, a continuación, se crea un usuario de base de datos correspondiente `AbolrousHazem` en `AdventureWorks2012`.  
  
```  
CREATE LOGIN AbolrousHazem   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
```   
Cambiar a una base de datos de usuario. Por ejemplo, en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizar el `USE AdventureWorks2012` instrucción. En [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], debe realizar una nueva conexión con la base de datos de usuario.

```   
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
GO   
```  
  
### <a name="b-creating-a-database-user-with-a-default-schema"></a>B. Crear un usuario de base de datos con un esquema predeterminado  
 En el siguiente ejemplo, primero se crea un inicio de sesión de servidor denominado `WanidaBenshoof` con una contraseña y, a continuación, se crea el usuario de base de datos `Wanida` correspondiente con el esquema predeterminado `Marketing`.  
  
```  
CREATE LOGIN WanidaBenshoof   
    WITH PASSWORD = '8fdKJl3$nlNv3049jsKK';  
USE AdventureWorks2012;  
CREATE USER Wanida FOR LOGIN WanidaBenshoof   
    WITH DEFAULT_SCHEMA = Marketing;  
GO  
```  
  
### <a name="c-creating-a-database-user-from-a-certificate"></a>C. Crear un usuario de base de datos a partir de un certificado  
 En el siguiente ejemplo, se crea el usuario de base de datos `JinghaoLiu` desde el certificado `CarnationProduction50`.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012;  
CREATE CERTIFICATE CarnationProduction50  
    WITH SUBJECT = 'Carnation Production Facility Supervisors',  
    EXPIRY_DATE = '11/11/2011';  
GO  
CREATE USER JinghaoLiu FOR CERTIFICATE CarnationProduction50;  
GO   
```  
  
###  <a name="withoutLogin"></a> D. Crear y utilizar un usuario sin inicio de sesión  
 En el ejemplo siguiente se crea un usuario de base de datos `CustomApp` que no se asigna a un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A continuación, se concede a un usuario el permiso `adventure-works\tengiz0` para suplantar al usuario de `CustomApp`.  
  
```  
USE AdventureWorks2012 ;  
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  
GO   
```  
  
 Para usar las credenciales de `CustomApp`, el usuario `adventure-works\tengiz0` ejecuta la siguiente instrucción.  
  
```  
EXECUTE AS USER = 'CustomApp' ;  
GO  
```  
  
 Para revertir a las credenciales de `adventure-works\tengiz0`, el usuario ejecuta la siguiente instrucción.  
  
```  
REVERT ;  
GO  
```  
  
### <a name="e-creating-a-contained-database-user-with-password"></a>E. Crear un usuario de base de datos independiente con contraseña  
 En el siguiente ejemplo se crea un usuario de base de datos independiente con contraseña. Este ejemplo solo se puede ejecutar en una base de datos independiente.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este ejemplo funciona en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] si se quita DEFAULT_LANGUAGE.  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
GO   
```  
  
### <a name="f-creating-a-contained-database-user-for-a-domain-login"></a>F. Crear un usuario de base de datos independiente para un inicio de sesión de dominio  
 En el siguiente ejemplo se crea un usuario de base de datos independiente para un inicio de sesión denominado Fritz en un dominio denominado Contoso. Este ejemplo solo se puede ejecutar en una base de datos independiente.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER [Contoso\Fritz] ;  
GO   
```  
  
### <a name="g-creating-a-contained-database-user-with-a-specific-sid"></a>G. Crear un usuario de base de datos independiente con un SID específico  
 En el siguiente ejemplo se crea un usuario de base de datos independiente y autenticado de SQL Server denominado CarmenW. Este ejemplo solo se puede ejecutar en una base de datos independiente.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+'  
, SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  
  
```  
  
### <a name="h-creating-a-user-to-copy-encrypted-data"></a>H. Crear un usuario para copiar los datos cifrados  
 En el ejemplo siguiente se crea un usuario que puede copiar los datos que está protegidos por la característica Always Encrypted de un conjunto de tablas, que contiene las columnas cifradas, a otro conjunto de tablas con columnas cifradas (en la misma o a otra base de datos).  Para obtener más información, consulte [migrar información confidencial protegida mediante Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
```  
CREATE USER [Chin]   
WITH   
      DEFAULT_SCHEMA = dbo  
    , ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;  
```  
  

## <a name="next-steps"></a>Pasos siguientes  
Una vez que se crea el usuario, considere la posibilidad de agregar el usuario a un rol de base de datos mediante la [ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md) instrucción.  
Puede que le interese a [otorgar permisos de objeto](../../t-sql/statements/grant-object-permissions-transact-sql.md) a la función para que pueden acceder a las tablas. Para obtener información general sobre el modelo de seguridad de SQL Server, vea [permisos](../../relational-databases/security/permissions-database-engine.md).   
  
## <a name="see-also"></a>Vea también  
 [Crear un usuario de base de datos](../../relational-databases/security/authentication-access/create-a-database-user.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [Eliminar usuario &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Bases de datos independientes](../../relational-databases/databases/contained-databases.md)   
 [Conectarse a la base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)   
 [Introducción a los permisos de los motores de bases de datos](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  



