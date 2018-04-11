---
title: sp_addlinkedsrvlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a4a55d2128cdba654ce9e753ac1cdcebd8f0ad8d
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/10/2018
---
# <a name="spaddlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea o actualiza una asignación entre un inicio de sesión en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una cuenta de seguridad en un servidor remoto.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] 'TRUE' | 'FALSE' | NULL ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @rmtsrvname **=** ] **'***rmtsrvname***'**  
 Es el nombre de un servidor vinculado al que se aplica la asignación de inicio de sesión. *rmtsrvname* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @useself **=** ] **'**TRUE**'** | 'FALSE' | 'NULL'  
 Determina si se debe conectar a *rmtsrvname* suplantando inicios de sesión locales o enviando explícitamente un inicio de sesión y una contraseña. El tipo de datos es **varchar (**8**)**, con un valor predeterminado es TRUE.  
  
 Un valor TRUE especifica que los inicios de sesión utilizan sus propias credenciales para conectarse a *rmtsrvname*, con el *rmtuser* y *rmtpassword* argumentos que se pasa por alto. FALSE especifica que la *rmtuser* y *rmtpassword* argumentos se utilizan para conectarse a *rmtsrvname* para el elemento especificado *locallogin* . Si *rmtuser* y *rmtpassword* también está establecido en NULL, ningún inicio de sesión o la contraseña se utiliza para conectarse al servidor vinculado.  
  
 [ @locallogin **=** ] **'***locallogin***'**  
 Es un inicio de sesión en el servidor local. *locallogin* es **sysname**, su valor predeterminado es null. NULL especifica que esta entrada se aplica a todos los inicios de sesión locales que se conectan a *rmtsrvname*. Si no es NULL, *locallogin* puede ser un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o un inicio de sesión de Windows. El inicio de sesión de Windows debe disponer de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya sea directamente o en calidad de miembro de un grupo de Windows al que se ha concedido acceso.  
  
 [ @rmtuser **=** ] **'***rmtuser***'**  
 Es el inicio de sesión remoto para conectarse a *rmtsrvname* cuando @useself es FALSE. Cuando el servidor remoto es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no usa la autenticación de Windows, *rmtuser* es un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión. *rmtuser* es **sysname**, su valor predeterminado es null.  
  
 [ @rmtpassword **=** ] **'***rmtpassword***'**  
 Es la contraseña asociada *rmtuser*. *rmtpassword* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Cuando un usuario inicia la sesión en el servidor local y ejecuta una consulta distribuida que obtiene acceso a una tabla del servidor vinculado, el servidor local debe iniciar la sesión en el servidor vinculado en nombre del usuario para obtener acceso a esa tabla. Utilice sp_addlinkedsrvlogin para especificar las credenciales de inicio de sesión que utiliza el servidor local para iniciar sesión en el servidor vinculado.  
  
> [!NOTE]  
>  Para crear los mejores planes de consulta cuando utiliza una tabla en un servidor vinculado, el procesador de consultas debe disponer de estadísticas de distribución de datos del servidor vinculado. Los usuarios con permisos limitados en las columnas de la tabla puede que no tengan permisos suficientes para obtener todas las estadísticas de utilidad, y puede que reciban un plan de consulta menos eficaz y experimenten un bajo rendimiento. Si el servidor vinculado es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para obtener todas las estadísticas disponibles, el usuario debe ser propietario de la tabla o miembro del rol fijo de servidor sysadmin, del rol fijo de base de datos db_owner o del rol fijo de base de datos db_ddladmin en el servidor vinculado. SQL Server 2012 SP1 modifica las restricciones de permisos para obtener estadísticas y permite a los usuarios que disponen del permiso SELECT tener acceso a las estadísticas disponibles mediante DBCC SHOW_STATISTICS. Para obtener más información, vea la sección de permisos de [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md).  
  
 Al ejecutar sp_addlinkedserver, se crea automáticamente una asignación predeterminada entre todos los inicios de sesión del servidor local y los inicios de sesión remotos del servidor vinculado. La asignación predeterminada indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza las credenciales de usuario del inicio de sesión local al conectarse al servidor vinculado en nombre del inicio de sesión. Esto equivale a ejecutar sp_addlinkedsrvlogin con @useself establecido en **true** para el servidor vinculado, sin especificar un nombre de usuario local. Utilice sp_addlinkedsrvlogin solo para cambiar la asignación predeterminada o para agregar asignaciones nuevas para inicios de sesión locales específicos. Para eliminar la asignación predeterminada o cualquier otra asignación, utilice sp_droplinkedsrvlogin.  
  
 En lugar de tener que usar sp_addlinkedsrvlogin para crear una asignación de inicio de sesión predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede utilizar automáticamente las credenciales de seguridad de Windows (nombre de inicio de sesión y contraseña de Windows) de un usuario que emita la consulta para conectarse a un servidor vinculado cuando se den todas estas condiciones:  
  
-   Un usuario se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el Modo de autenticación de Windows.  
  
-   La delegación de cuentas de seguridad está disponible en el cliente y en el servidor de envío.  
  
-   El proveedor admite el Modo de autenticación de Windows (por ejemplo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en Windows).  
  
> [!NOTE]  
>  La delegación no tiene que estar habilitada en escenarios de un solo salto, pero es necesaria en escenarios de varios saltos.  
  
 Cuando el servidor vinculado ya ha realizado la autenticación utilizando las asignaciones que se definen al ejecutar sp_addlinkedsrvlogin en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los permisos para cada objeto individual de la base de datos remota los determina el servidor vinculado, no el servidor local.  
  
 sp_addlinkedsrvlogin no se puede ejecutar desde una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. Conectar todos los inicios de sesión locales al servidor vinculado mediante sus propias credenciales de usuario  
 En el ejemplo siguiente se crea una asignación para asegurar que todos los inicios de sesión en el servidor local se conectan a través del servidor vinculado `Accounts` mediante sus propias credenciales de usuario.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 O bien  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  Si hay asignaciones explícitas creadas para inicios de sesión individuales, éstas tienen prioridad sobre cualquier asignación global que exista para ese servidor vinculado.  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. Conectar un inicio de sesión específico al servidor vinculado mediante credenciales de usuario distintas  
 En el ejemplo siguiente se crea una asignación para asegurar que solo el usuario de Windows `Domain\Mary` se conecta a través del servidor vinculado `Accounts` mediante el inicio de sesión `MaryP` y la contraseña `d89q3w4u`.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  En este ejemplo no se utiliza la autenticación de Windows. Las contraseñas se transmiten sin cifrar. Las contraseñas pueden verse en las definiciones de origen de datos y scripts que se guardan en el disco, en las copias de seguridad y en archivos de registro. No utilice nunca una contraseña de administrador en este tipo de conexión. Solicite a su administrador de red directrices de seguridad específicas para este entorno.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de servidores vinculados &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
