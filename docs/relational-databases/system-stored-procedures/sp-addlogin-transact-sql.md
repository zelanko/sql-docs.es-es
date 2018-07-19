---
title: sp_addlogin (Transact-SQL) | Microsoft Docs
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
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5f9458c1459aef35bcf9d6e47963025f87000c32
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060160"
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuevo inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite a un usuario conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) en su lugar.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame=] '*inicio de sesión*'  
 Es el nombre del inicio de sesión. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @passwd=] '*contraseña*'  
 Es la contraseña de inicio de sesión. *contraseña* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*base de datos*'  
 Es la base de datos predeterminada del inicio de sesión (la base de datos a la que primero se conecta el inicio de sesión después de iniciarse la sesión). *base de datos* es **sysname**, su valor predeterminado es **maestro**.  
  
 [ @deflanguage=] '*lenguaje*'  
 Es el idioma predeterminado del inicio de sesión. *lenguaje* es **sysname**, su valor predeterminado es null. Si *lenguaje* no se especifica, el valor predeterminado *lenguaje* del nuevo inicio de sesión se establece en el idioma predeterminado actual del servidor.  
  
 [ @sid=] '*sid*'  
 Especifica el número de identificación de seguridad (SID). *SID* es **varbinary (16)**, su valor predeterminado es null. Si *sid* es NULL, el sistema genera un SID para el nuevo inicio de sesión. A pesar del uso de un **varbinary** tipo de datos, los valores distintos de NULL deben tener exactamente 16 bytes de longitud y no debe existir. Especificar *sid* es útil, por ejemplo, cuando se cifran o mueven [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión de un servidor a otro y desean que los inicios de sesión tienen el mismo SID en servidores diferentes.  
  
 [ @encryptopt=] '*encryption_option*'  
 Especifica si la contraseña se pasa como texto sin cifrar o como hash de la contraseña de texto sin cifrar. Tenga en cuenta que no se realiza el cifrado. La palabra "cifrar" se utiliza aquí para la compatibilidad con versiones anteriores. Si se pasa una contraseña de texto sin cifrar, está en formato hash. El hash se almacena. *encryption_option* es **varchar (20)**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|NULL|La contraseña se pasa como texto sin cifrar. Ésta es la opción predeterminada.|  
|**skip_encryption**|La contraseña ya está en formato hash. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe almacenar el valor sin volver a procesar el hash de la contraseña.|  
|**skip_encryption_old**|La contraseña proporcionada estaba en formato hash en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe almacenar el valor sin volver a procesar el hash de la contraseña. Esta opción solo se proporciona para permitir la actualización.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Notas  
 Los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden contener entre 1 y 128 caracteres, y pueden incluir letras, símbolos y números. Los inicios de sesión no pueden contener una barra diagonal inversa (\\); ser un nombre de inicio de sesión reservado, por ejemplo sa o public, o ya existe; o ser NULL ni una cadena vacía (`''`).  
  
 Si se proporciona el nombre de una base de datos predeterminada, puede conectarse a la base de datos especificada sin ejecutar la instrucción USE. Sin embargo, no se puede usar la base de datos predeterminada hasta que se tiene acceso a esa base de datos por el propietario de la base de datos (mediante el uso de [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) o [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) o [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 El número de SID es un GUID que identificará de forma exclusiva el inicio de sesión en el servidor.  
  
 Al cambiar el idioma predeterminado del servidor no se cambia el idioma predeterminado de los inicios de sesión existentes. Para cambiar el idioma predeterminado del servidor, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Uso de **skip_encryption** para suprimir la contraseña hash es útil si la contraseña ya está en hash cuando se agrega el inicio de sesión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la contraseña estaba en formato hash en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilice **skip_encryption_old**.  
  
 sp_addlogin no se puede ejecutar desde una transacción definida por el usuario.  
  
 En la siguiente tabla se muestran varios procedimientos almacenados que se utilizan con sp_addlogin.  
  
|Procedimiento almacenado|Descripción|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Agrega un usuario o grupo de Windows.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|Cambia la contraseña de un usuario.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|Cambia la base de datos predeterminada de un usuario.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|Cambia el idioma predeterminado de un usuario.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY LOGIN.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-sql-server-login"></a>A. Crear un inicio de sesión de SQL Server  
 En el siguiente ejemplo se crea un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el usuario `Victoria`, con una contraseña `B1r12-36`, sin especificar una base de datos predeterminada.  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. Crear un inicio de sesión de SQL Server que tiene una base de datos predeterminada  
 En el siguiente ejemplo se crea un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el usuario `Albert`, con una contraseña `B5432-3M6` y una base de datos predeterminada `corporate`.  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. Crear un inicio de sesión de SQL Server que tiene otro idioma predeterminado  
 En el siguiente ejemplo se crea un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el usuario `TzTodorov`, con una contraseña `709hLKH7chjfwv`, una base de datos predeterminada `AdventureWorks2012` y un idioma predeterminado `Bulgarian`.  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. Crear un inicio de sesión de SQL Server que tiene un SID específico  
 En el siguiente ejemplo se crea un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el usuario `Michael`, con una contraseña `B548bmM%f6`, una base de datos predeterminada `AdventureWorks2012`, un idioma predeterminado `us_english` y un SID `0x0123456789ABCDEF0123456789ABCDEF`.  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
