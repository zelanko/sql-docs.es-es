---
title: ALTER LOGIN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/01/2017
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
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9dd47cb63c56dbbfb5f31ea3f7b2c8d4f45e9d73
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
-- Syntax for Azure SQL Database  
  
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
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
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
 Habilita o deshabilita este inicio de sesión. Deshabilitar un inicio de sesión no afecta al comportamiento de los inicios de sesión que ya están conectados. (Use el `KILL` instrucción para terminar las conexiones existentes.) Los inicios de sesión deshabilitados conservan sus permisos y pueden seguir siendo suplantados.  
  
 CONTRASEÑA **='***contraseña***'**  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica la contraseña del inicio de sesión que se está cambiando. En las contraseñas se distingue entre mayúsculas y minúsculas.  
  
 Continuamente las conexiones activas con la base de datos SQL requieren vuelva a autorizarla (realizada por el motor de base de datos) al menos cada 10 horas. El motor de base de datos intenta vuelva a autorizarla con la contraseña enviada originalmente e intervención del usuario no es obligatorio. Por motivos de rendimiento cuando se restablece una contraseña de base de datos de SQL, la conexión no se volverá a autenticar, incluso si la conexión se restablezca debido a la agrupación de conexiones. Esto es diferente del comportamiento del servidor local de SQL. Si la contraseña se cambió desde que inicialmente se autorizó la conexión, debe terminar la conexión y establece una nueva conexión con la nueva contraseña. Un usuario con el permiso KILL DATABASE CONNECTION puede finalizar explícitamente una conexión a la base de datos SQL mediante el comando KILL. Para obtener más información, vea [KILL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/kill-transact-sql.md).  
  
 CONTRASEÑA  **=**  *hashed_password*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a la palabra clave HASHED. Especifica el valor con hash de la contraseña para el inicio de sesión que se está creando.  
  
> [!IMPORTANT]  
>  Cuando un inicio de sesión (o un usuario de base de datos independiente) se conecta y se autentica, la conexión almacena en memoria caché información de identidad del inicio de sesión. Para un inicio de sesión con autenticación de Windows, esto incluye la información sobre la pertenencia a grupos de Windows. La identidad del inicio de sesión permanecerá autenticada mientras dure la conexión. Para aplicar cambios en la identidad, como un cambio o restablecimiento de contraseña de la pertenencia al grupo de Windows, el inicio de sesión debe cerrar sesión en la entidad de autenticación (Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) y volver a iniciar sesión. Los miembros del rol fijo de servidor **sysadmin** o cualquier inicio de sesión con el permiso **ALTER ANY CONNECTION** puede usar el comando **KILL** para finalizar una conexión y hacer que el inicio de sesión se vuelva a conectar. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede reutilizar la información de conexión al abrir varias conexiones en las ventanas del Explorador de objetos y del Editor de consultas. Cierre todas las conexiones para forzar una reconexión.  
  
 HASHED  
   
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Se aplica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo inicios de sesión. Especifica que la contraseña especificada después del argumento PASSWORD ya tiene aplicado el algoritmo hash. Si no se selecciona esta opción, se aplica un algoritmo hash a la contraseña antes de almacenarla en la base de datos. Esta opción solo se debería utilizar para la sincronización del inicio de sesión entre dos servidores. No utilice la opción HASHED para cambiar las contraseñas de forma habitual.  
  
 Contraseña_anterior **='***oldpassword***'**  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La contraseña actual del inicio de sesión al que se va a asignar una contraseña nueva. En las contraseñas se distingue entre mayúsculas y minúsculas.  
  
 MUST_CHANGE  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si se incluye esta opción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pedirá la contraseña actualizada la primera vez que se utilice el inicio de sesión modificado.  
  
 DEFAULT_DATABASE  **=**  *base de datos*  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica una base de datos predeterminada que debe asignarse al inicio de sesión.  
  
 DEFAULT_LANGUAGE  **=**  *idioma*  
 
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el idioma predeterminado que debe asignarse al inicio de sesión. El idioma predeterminado para todos los inicios de sesión de base de datos SQL es el inglés y no se puede cambiar. El idioma predeterminado de la `sa` inicio de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Linux, es el inglés, pero se puede cambiar.  
  
 NOMBRE = *login_name*  
 Especifica el nombre nuevo del inicio de sesión al que se está cambiando el nombre. Si se trata de un inicio de sesión de Windows, el SID de la entidad de seguridad de Windows correspondiente al nombre nuevo debe coincidir con el SID asociado al inicio de sesión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El nuevo nombre de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión no puede contener un carácter de barra diagonal inversa (\\).  
  
 CHECK_EXPIRATION = {ON | **OFF** }  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica si debe aplicarse la directiva de caducidad de contraseñas en este inicio de sesión. El valor predeterminado es OFF.  
  
 CHECK_POLICY  **=**  { **ON** | {OFF}  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que se deben aplicar las directivas de contraseñas de Windows en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este inicio de sesión. El valor predeterminado es ON.  
  
 CREDENCIAL = *credential_name*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 El nombre de una credencial que debe asignarse a un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La credencial debe existir en la base de datos. Para obtener más información, consulte [credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md). No se puede asignar una credencial para el inicio de sesión de sa.  
  
 NO CREDENTIAL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Elimina cualquier asignación existente del inicio de sesión a una credencial de servidor. Para obtener más información, consulte [credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 UNLOCK  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Solo se aplica a inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que un inicio de sesión bloqueado debe desbloquearse.  
  
 ADD CREDENTIAL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Agrega una credencial del proveedor de Administración extensible de claves (EKM) al inicio de sesión. Para obtener más información, vea [administración Extensible de claves &#40; EKM &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
 DROP CREDENTIAL  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
Quita una credencial de proveedor de administración Extensible de claves (EKM) desde el inicio de sesión. Para obtener más información consulte [administración Extensible de claves &#40; EKM &#41; ](../../relational-databases/security/encryption/extensible-key-management-ekm.md).  
  
## <a name="remarks"></a>Comentarios  
 Cuando CHECK_POLICY se establece en ON, no puede utilizarse el argumento HASHED.  
  
 Cuando el valor de CHECK_POLICY se cambia a ON, ocurre lo siguiente:  
  
-   El historial de contraseñas se inicializa con el valor del hash de contraseña actual.  
  
 Cuando CHECK_POLICY se cambia a OFF, ocurre lo siguiente:  
  
-   La opción CHECK_EXPIRATION también se cambia a OFF.  
  
-   Se borra el historial de contraseñas.  
  
-   El valor de *lockout_time* se restablece.  
  
Si se especifica MUST_CHANGE, CHECK_EXPIRATION y CHECK_POLICY, deben establecerse en ON. Si no es así, la instrucción producirá un error.  
  
Si CHECK_POLICY se establece en OFF, CHECK_EXPIRATION no puede establecerse en ON. Una instrucción ALTER LOGIN con esta combinación de opciones dará error.  
  
No puede usar ALTER_LOGIN con el argumento DISABLE para denegar el acceso a un grupo de Windows. Por ejemplo, ALTER_LOGIN [*domain\group*] DISABLE devolverá el mensaje de error siguiente:  
  
 "Mensaje 15151, nivel 16, estado 1, línea 1"  
  
 "No se puede modificar el inicio de sesión '*Domain\Group*', porque no existe o no tiene permiso."  
  
 es así por diseño.  
  
En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], datos de inicio de sesión necesitan para autenticar una conexión y las reglas de firewall de nivel de servidor se almacenan temporalmente en caché en cada base de datos. Esta caché se actualiza periódicamente. Para forzar una actualización de la caché de autenticación y asegúrese de que una base de datos tiene la versión más reciente de la tabla de inicios de sesión, ejecute [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN.  
  
 Si se utiliza la opción CREDENTIAL, también será necesario el permiso ALTER ANY CREDENTIAL.  
  
 Si el inicio de sesión que se va a cambiar es un miembro de la **sysadmin** rol fijo de servidor o tiene concedido el permiso CONTROL SERVER, también requiere el permiso CONTROL SERVER al realizar los siguientes cambios:  
  
-   Restablecer la contraseña sin proporcionar la antigua.  
  
-   Habilitar MUST_CHANGE, CHECK_POLICY o CHECK_EXPIRATION.  
  
-   Cambiar el nombre de inicio de sesión.  
  
-   Habilitar o deshabilitar el inicio de sesión.  
  
-   Asignar el inicio de sesión a una credencial diferente.  
  
 Una entidad de seguridad puede cambiar la contraseña, el idioma predeterminado y la base de datos predeterminada para su propio inicio de sesión.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enabling-a-disabled-login"></a>A. Habilitar un inicio de sesión deshabilitado  
 En el ejemplo siguiente se habilita el inicio de sesión `Mary5`.  
  
```tsql  
ALTER LOGIN Mary5 ENABLE;  
```  
  
### <a name="b-changing-the-password-of-a-login"></a>B. Cambiar la contraseña de un inicio de sesión  
 En el ejemplo siguiente se cambia la contraseña del inicio de sesión `Mary5` a una contraseña segura.  
  
```tsql  
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
### <a name="c-changing-the-name-of-a-login"></a>C. Cambiar el nombre de un inicio de sesión  
 En el ejemplo siguiente se cambia el nombre del inicio de sesión `Mary5` a `John2`.  
  
```tsql  
ALTER LOGIN Mary5 WITH NAME = John2;  
```  
  
### <a name="d-mapping-a-login-to-a-credential"></a>D. Asignar un inicio de sesión a una credencial  
 En el ejemplo siguiente se asigna el inicio de sesión `John2` a la credencial `Custodian04`.  
  
```tsql  
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;  
```  
  
### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Asignar un inicio de sesión a una credencial de Administración de claves extensible  
 En el ejemplo siguiente se asigna el inicio de sesión `Mary5` a la credencial EKM `EKMProvider1`.  
  
 
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```tsql  
ALTER LOGIN Mary5  
ADD CREDENTIAL EKMProvider1;  
GO  
```  
  
### <a name="f-unlocking-a-login"></a>F. Desbloquear un inicio de sesión  
 Para desbloquear un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecute la instrucción siguiente, reemplazando **** con la contraseña de cuenta deseada.  
  
  
```tsql  
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;  

GO  
```  
  
 Para desbloquear un inicio de sesión sin cambiar la contraseña, desactive la directiva de comprobación y, a continuación, inicie sesión de nuevo.  
  
```tsql  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;  
GO  
```  
  
### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Cambiar la contraseña de un inicio de sesión utilizando HASHED  
 En el ejemplo siguiente se cambia la contraseña de inicio de sesión de `TestUser` a un valor que ya tiene aplicado hash.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```tsql  
ALTER LOGIN TestUser WITH   
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;  
GO  
```  
  
 
  
## <a name="see-also"></a>Vea también  
 [Credenciales &#40; motor de base de datos &#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [QUITAR el inicio de sesión &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Administración extensible de claves &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  



