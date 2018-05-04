---
title: ALTER LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_LOGIN_TSQL
- ALTER LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER LOGIN statement
- change password
- mapping logins [SQL Server]
- logins [SQL Server], modifying
- passwords [SQL Server], modifying
- names [SQL Server], logins
- modifying login accounts
ms.assetid: e247b84e-c99e-4af8-8b50-57586e1cb1c5
caps.latest.revision: 68
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d1a1bbef130ca5b5fef4255121a8d602c9dc47d2
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="alter-login-transact-sql"></a>ALTER LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cambia las propiedades de una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    | <cryptographic_credential_option>  
    }   
[;]  
  
<status_option> ::=  
        ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD = 'password' | hashed_password HASHED  
    [   
      OLD_PASSWORD = 'oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }  
    | CREDENTIAL = credential_name  
    | NO CREDENTIAL  
  
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
  
<cryptographic_credentials_option> ::=   
    ADD CREDENTIAL credential_name  
  | DROP CREDENTIAL credential_name  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse 
  
ALTER LOGIN login_name   
  {   
      <status_option>   
    | WITH <set_option> [ ,.. .n ]   
  }   
[;]  
  
<status_option> ::=  
    ENABLE | DISABLE  
  
<set_option> ::=   
    PASSWORD ='password'   
    [  
      OLD_PASSWORD ='oldpassword'  
    ]   
    | NAME = login_name  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    }   
  
<status_option> ::=ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD ='password'   
    [   
      OLD_PASSWORD ='oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }   
      
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
```  
  
## <a name="arguments"></a>Argumentos  
 *login_name*  
 Especifica el nombre del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se está cambiando. Los inicios de sesión del dominio se deben incluir entre corchetes con el formato [dominio\usuario].  
  
 ENABLE | DISABLE  
 Habilita o deshabilita este inicio de sesión. Deshabilitar un inicio de sesión no afecta al comportamiento de los inicios de sesión que ya están conectados. (Use la instrucción `KILL` para finalizar las conexiones existentes). Los inicios de sesión deshabilitados conservan sus permisos y pueden seguir siendo suplantados.  
  
 PASSWORD **='***password***'**  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica la contraseña del inicio de sesión que se está cambiando. En las contraseñas se distingue entre mayúsculas y minúsculas.  
  
 Las conexiones continuamente activas a SQL Database requieren una reautorización (realizada por el Motor de base de datos) como mínimo cada 10 horas. El Motor de base de datos intenta la reautorización con la contraseña enviada originalmente y no se requiere la intervención del usuario. Por motivos de rendimiento, cuando una contraseña se restablece en SQL Database, la conexión no se volverá a autenticar, incluso si se restablece la conexión debido a la agrupación de conexiones. Esto es diferente del comportamiento de SQL Database local. Si la contraseña se ha cambiado desde que se autorizó inicialmente la conexión, es necesario terminar la conexión y establecer una nueva conexión con la nueva contraseña. Un usuario con el permiso KILL DATABASE CONNECTION puede terminar explícitamente una conexión con SQL Database mediante el comando KILL. Para obtener más información, consulte [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md).  
  
 PASSWORD **=***hashed_password*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a la palabra clave HASHED. Especifica el valor con hash de la contraseña para el inicio de sesión que se está creando.  
  
> [!IMPORTANT]  
>  Cuando un inicio de sesión (o un usuario de base de datos independiente) se conecta y se autentica, la conexión almacena en memoria caché información de identidad del inicio de sesión. Para un inicio de sesión con autenticación de Windows, esto incluye la información sobre la pertenencia a grupos de Windows. La identidad del inicio de sesión permanecerá autenticada mientras dure la conexión. Para aplicar cambios en la identidad, como un cambio o restablecimiento de contraseña de la pertenencia al grupo de Windows, el inicio de sesión debe cerrar sesión en la entidad de autenticación (Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) y volver a iniciar sesión. Los miembros del rol fijo de servidor **sysadmin** o cualquier inicio de sesión con el permiso **ALTER ANY CONNECTION** puede usar el comando **KILL** para finalizar una conexión y hacer que el inicio de sesión se vuelva a conectar. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede reutilizar la información de conexión al abrir varias conexiones en las ventanas del Explorador de objetos y del Editor de consultas. Cierre todas las conexiones para forzar una reconexión.  
  
 HASHED  
   
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que la contraseña especificada después del argumento PASSWORD ya tiene aplicado el algoritmo hash. Si no se selecciona esta opción, se aplica un algoritmo hash a la contraseña antes de almacenarla en la base de datos. Esta opción solo se debería utilizar para la sincronización del inicio de sesión entre dos servidores. No utilice la opción HASHED para cambiar las contraseñas de forma habitual.  
  
 OLD_PASSWORD **='***oldpassword***'**  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La contraseña actual del inicio de sesión al que se va a asignar una contraseña nueva. En las contraseñas se distingue entre mayúsculas y minúsculas.  
  
 MUST_CHANGE  
 **Se aplica a**: de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y a Almacenamiento de datos paralelos.  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se incluye esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pedirá la contraseña actualizada la primera vez que se utilice el inicio de sesión modificado.  
  
 DEFAULT_DATABASE **=***database*  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica una base de datos predeterminada que debe asignarse al inicio de sesión.  
  
 DEFAULT_LANGUAGE **=***language*  
 
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el idioma predeterminado que debe asignarse al inicio de sesión. El idioma predeterminado para todos los inicios de sesión de SQL Database es el inglés y no se puede cambiar. El idioma predeterminado del inicio de sesión de `sa` en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Linux es el inglés, pero se puede cambiar.  
  
 NAME = *login_name*  
 Especifica el nombre nuevo del inicio de sesión al que se está cambiando el nombre. Si se trata de un inicio de sesión de Windows, el SID de la entidad de seguridad de Windows correspondiente al nombre nuevo debe coincidir con el SID asociado al inicio de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El nombre nuevo de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede contener un carácter de barra diagonal inversa (\\).  
  
 CHECK_EXPIRATION = { ON | **OFF** }  
 **Se aplica a**: de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y a Almacenamiento de datos paralelos.  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica si debe aplicarse la directiva de caducidad de contraseñas en este inicio de sesión. El valor predeterminado es OFF.  
  
 CHECK_POLICY **=** { **ON** | OFF }  
 **Se aplica a**: de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y a Almacenamiento de datos paralelos.  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que se deben aplicar las directivas de contraseñas de Windows en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este inicio de sesión. El valor predeterminado es ON.  
  
 CREDENTIAL = *credential_name*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 El nombre de una credencial que debe asignarse a un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La credencial debe existir en la base de datos. Para obtener más información, vea [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). Las credenciales no se pueden asignar al inicio de sesión sa.  
  
 NO CREDENTIAL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Elimina cualquier asignación existente del inicio de sesión a una credencial de servidor. Para obtener más información, vea [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 UNLOCK  
 **Se aplica a**: de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y a Almacenamiento de datos paralelos.  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que un inicio de sesión bloqueado debe desbloquearse.  
  
 ADD CREDENTIAL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Agrega una credencial del proveedor de Administración extensible de claves (EKM) al inicio de sesión. Para obtener más información, vea [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 DROP CREDENTIAL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Quita una credencial del proveedor de Administración extensible de claves (EKM) en el inicio de sesión. Para obtener más información, vea [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Notas  
 Cuando CHECK_POLICY se establece en ON, no puede utilizarse el argumento HASHED.  
  
 Cuando el valor de CHECK_POLICY se cambia a ON, ocurre lo siguiente:  
  
-   El historial de contraseñas se inicializa con el valor del hash de contraseña actual.  
  
 Cuando el valor de CHECK_POLICY se cambia a OFF, ocurre lo siguiente:  
  
-   La opción CHECK_EXPIRATION también se cambia a OFF.  
  
-   Se borra el historial de contraseñas.  
  
-   El valor de *lockout_time* se restablece.  
  
Si se especifica MUST_CHANGE, CHECK_EXPIRATION y CHECK_POLICY, deben establecerse en ON. Si no es así, la instrucción producirá un error.  
  
Si CHECK_POLICY se establece en OFF, CHECK_EXPIRATION no puede establecerse en ON. Una instrucción ALTER LOGIN con esta combinación de opciones dará error.  
  
No puede usar ALTER_LOGIN con el argumento DISABLE para denegar el acceso a un grupo de Windows. Por ejemplo, ALTER_LOGIN [*domain\group*] DISABLE devolverá el siguiente mensaje de error:  
  
 "Mensaje 15151, nivel 16, estado 1, línea 1"  
  
 "No se puede modificar el inicio de sesión '*Domain\Group*' porque no existe o no tiene permisos".  
  
 es así por diseño.  
  
En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], los datos de inicio de sesión necesarios para autenticar una conexión y reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza regularmente. Para forzar una actualización de la caché de autenticación y garantizar que una base de datos tenga la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY LOGIN.  
  
 Si se utiliza la opción CREDENTIAL, también será necesario el permiso ALTER ANY CREDENTIAL.  
  
 Si el inicio de sesión que se está cambiado es un miembro del rol fijo de servidor **sysadmin** o tiene concedido el permiso CONTROL SERVER, también será necesario el permiso CONTROL SERVER para realizar los cambios siguientes:  
  
-   Restablecer la contraseña sin proporcionar la antigua.  
  
-   Habilitar MUST_CHANGE, CHECK_POLICY o CHECK_EXPIRATION.  
  
-   Cambiar el nombre de inicio de sesión.  
  
-   Habilitar o deshabilitar el inicio de sesión.  
  
-   Asignar el inicio de sesión a una credencial diferente.  
  
 Una entidad de seguridad puede cambiar la contraseña, el idioma predeterminado y la base de datos predeterminada para su propio inicio de sesión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enabling-a-disabled-login"></a>A. Habilitar un inicio de sesión deshabilitado  
 En el ejemplo siguiente se habilita el inicio de sesión `Mary5`.  
  
```sql  
ALTER LOGIN Mary5 ENABLE;  
```  
  
### <a name="b-changing-the-password-of-a-login"></a>B. Cambiar la contraseña de un inicio de sesión  
 En el ejemplo siguiente se cambia la contraseña del inicio de sesión `Mary5` a una contraseña segura.  
  
```sql  
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
### <a name="c-changing-the-name-of-a-login"></a>C. Cambiar el nombre de un inicio de sesión  
 En el ejemplo siguiente se cambia el nombre del inicio de sesión `Mary5` a `John2`.  
  
```sql  
ALTER LOGIN Mary5 WITH NAME = John2;  
```  
  
### <a name="d-mapping-a-login-to-a-credential"></a>D. Asignar un inicio de sesión a una credencial  
 En el ejemplo siguiente se asigna el inicio de sesión `John2` a la credencial `Custodian04`.  
  
```sql  
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;  
```  
  
### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Asignar un inicio de sesión a una credencial de Administración de claves extensible  
 En el ejemplo siguiente se asigna el inicio de sesión `Mary5` a la credencial EKM `EKMProvider1`.  
  
 
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
ALTER LOGIN Mary5  
ADD CREDENTIAL EKMProvider1;  
GO  
```  
  
### <a name="f-unlocking-a-login"></a>F. Desbloquear un inicio de sesión  
 Para desbloquear un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecute la instrucción siguiente, reemplazando **** con la contraseña de cuenta deseada.  
  
  
```sql  
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;  

GO  
```  
  
 Para desbloquear un inicio de sesión sin cambiar la contraseña, desactive la directiva de comprobación y, a continuación, inicie sesión de nuevo.  
  
```sql  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;  
GO  
```  
  
### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Cambiar la contraseña de un inicio de sesión utilizando HASHED  
 En el ejemplo siguiente se cambia la contraseña de inicio de sesión de `TestUser` a un valor que ya tiene aplicado hash.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
ALTER LOGIN TestUser WITH   
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;  
GO  
```  
  
 
  
## <a name="see-also"></a>Ver también  
 [Credenciales &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  


