---
title: IS_SRVROLEMEMBER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: 65
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c26c0c1f4cb6a22f50cdc6a87d7a31f25b65e138
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Indica si en el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es miembro del rol de servidor especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *rol* **'**  
 Es el nombre del rol de servidor que se va comprobar. *rol* es **sysname**.  
  
 Los valores válidos para *rol* son roles de servidor definidos por el usuario y los siguientes roles fijos de servidor:  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> public|  
|processadmin||  
  
 **'** *inicio de sesión* **'**  
 Es el nombre de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión para comprobar. *inicio de sesión* es **sysname**, su valor predeterminado es null. Si no se especifica ningún valor, el resultado se basa en el contexto de ejecución actual. Si el parámetro contiene la palabra NULL, se devolverá NULL.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0|*inicio de sesión* no es un miembro de *rol*.<br /><br /> En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], esta instrucción siempre devuelve 0.|  
|1|*inicio de sesión* es un miembro de *rol*.|  
|NULL|*rol* o *inicio de sesión* no es válida, o no tiene permiso para ver la pertenencia al rol.|  
  
## <a name="remarks"></a>Comentarios  
 UseIS_SRVROLEMEMBER para determinar si el usuario actual puede realizar una acción que necesite permisos del rol de servidor.  
  
 Si se especifica un inicio de sesión de Windows, como Contoso\Mary5, para *inicio de sesión*, **IS_SRVROLEMEMBER** devuelve **NULL**, a menos que el inicio de sesión se ha concedido o denegado el acceso directo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si la parte opcional *inicio de sesión* parámetro es no siempre y si *inicio de sesión* es un inicio de sesión de dominio de Windows, puede ser un miembro del rol fijo de servidor mediante la pertenencia a un grupo de Windows. Para resolver estas pertenencias indirectas, IS_SRVROLEMEMBER solicita al controlador de dominio información sobre la pertenencia a grupos de Windows. Si el controlador de dominio es inaccesible o no responde, **IS_SRVROLEMEMBER** devuelve información de pertenencia a roles dando cuenta para el usuario y sus grupos locales solo. Si el usuario especificado no es el usuario actual, el valor devuelto por IS_SRVROLEMEMBER podría diferir de la última actualización de datos del autenticador (por ejemplo, Active Directory) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si se proporciona el parámetro de inicio de sesión opcional, el inicio de sesión de Windows que se consulta se debe encontrar en sys.server_principals o IS_SRVROLEMEMBER devolverá NULL. Esto indica que el inicio de sesión no es válido.  
  
 Cuando el parámetro de inicio de sesión es un inicio de sesión del dominio o está basado en un grupo de Windows y el controlador de dominio no es accesible, se producirá un error en las llamadas a IS_SRVROLEMEMBER y podrían devolverse datos incorrectos o incompletos.  
  
 Si el controlador de dominio no está disponible, la llamada a IS_SRVROLEMEMBER devolverá la información precisa cuando se puede autenticar el principio de Windows localmente, como una cuenta de Windows local o un inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **IS_SRVROLEMEMBER** siempre devuelve 0 cuando se utiliza un grupo de Windows como el argumento de inicio de sesión, y este grupo de Windows es un miembro de otro grupo de Windows que, a su vez, es un miembro del rol de servidor especificado.  
  
 La configuración de Control de cuentas de usuario (UAC) también puede provocar la devuelven resultados diferentes. Esto dependería de si el usuario tuvo acceso al servidor como un miembro del grupo de Windows o como un usuario específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta función evalúa la pertenencia al rol, no el permiso subyacente. Por ejemplo, el **sysadmin** rol fijo de servidor tiene la **CONTROL SERVER** permiso. Si el usuario tiene la **CONTROL SERVER** permiso pero no es un miembro del rol, esta función informará correctamente que el usuario no es un miembro de la **sysadmin** rol, aunque el usuario tiene el mismo permisos.  
  
## <a name="related-functions"></a>Funciones relacionadas  
 Para determinar si el usuario actual es miembro del grupo de Windows especificado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol de base de datos, utilice [IS_MEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). Para determinar si un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión es un miembro de un rol de base de datos, use [IS_ROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW DEFINITION en el rol de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se indica si el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el usuario actual es miembro del rol fijo de servidor `sysadmin`.  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 En el ejemplo siguiente se indica si el inicio de sesión de dominio Pat es un miembro de la **diskadmin** rol fijo de servidor.  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>Vea también  
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

