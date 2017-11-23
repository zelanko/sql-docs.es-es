---
title: IS_ROLEMEMBER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_ROLEMEMBER
- IS_ROLEMEMBER_TSQL
dev_langs: TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_ROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 73efa688-ae91-4014-98bc-1cabe47321f7
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd8574c27bea00127096dc1f0040c8c3f93e96cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Indica si una entidad de seguridad de base de datos especificada es miembro del rol de base de datos especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *rol* **'**  
 Nombre del rol de base de datos que se va comprobar. *rol* es **sysname**.  
  
 **'** *database_principal* **'**  
 Nombre del usuario de la base de datos, rol de base de datos o rol de aplicación que se va a comprobar. *database_principal* es **sysname**, su valor predeterminado es null. Si no se especifica ningún valor, el resultado se basa en el contexto de ejecución actual. Si el parámetro contiene la palabra NULL, se devolverá NULL.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0|*database_principal* no es un miembro de *rol*.|  
|1|*database_principal* es un miembro de *rol*.|  
|NULL|*database_principal* o *rol* no es válida, o no tiene permiso para ver la pertenencia al rol.|  
  
## <a name="remarks"></a>Comentarios  
 Utilice IS_ROLEMEMBER para determinar si el usuario actual puede realizar una acción que necesite los permisos del rol de base de datos.  
  
 Si *database_principal* se basa en un inicio de sesión de Windows, como Contoso\Mary5, IS_ROLEMEMBER devuelve NULL, a menos que la *database_principal* se ha concedido o denegado el acceso directo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si la parte opcional *database_principal* parámetro es no suministrada y, si la *database_principal* se basa en un inicio de sesión de dominio de Windows, puede ser un miembro de un rol de base de datos mediante la pertenencia a un grupo de Windows . Para resolver estas pertenencias indirectas, IS_ROLEMEMBER solicita al controlador de dominio información sobre la pertenencia a grupos de Windows. Si no se puede tener acceso al controlador de dominio o no responde, IS_ROLEMEMBER devuelve información sobre la pertenencia a roles teniendo en cuenta únicamente al usuario y sus grupos locales. Si el usuario especificado no es el usuario actual, el valor devuelto por IS_ROLEMEMBER podría diferir de la última actualización de datos del autenticador (por ejemplo, Active Directory) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si la parte opcional *database_principal* se proporciona el parámetro, la entidad de seguridad de base de datos que se está consultando debe estar presente en sys.database_principals o IS_ROLEMEMBER devolverá NULL. Esto indica que la *database_principal* no es válido en esta base de datos.  
  
 Cuando el *database_principal* parámetro se basa en un inicio de sesión de dominio o basado en un grupo de Windows y el controlador de dominio es accesible, se producirá un error las llamadas a IS_ROLEMEMBER y podrían devolverse datos incorrectos o incompletos.  
  
 Si el controlador de dominio no está disponible, la llamada a IS_ROLEMEMBER devolverá información precisa cuando se pueda autenticar localmente la entidad de seguridad de Windows, como una cuenta de Windows local o un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **IS_ROLEMEMBER** siempre devuelve 0 cuando se utiliza un grupo de Windows como el argumento de entidad de seguridad de base de datos, y este grupo de Windows es un miembro de otro grupo de Windows que, a su vez, es un miembro del rol de base de datos especificada.  
  
 El Control de cuentas de usuario (UAC) se encuentra en [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] y Windows Server 2008 también podrían devolver resultados diferentes. Esto dependería de si el usuario tuvo acceso al servidor como un miembro del grupo de Windows o como un usuario específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta función evalúa la pertenencia al rol, no el permiso subyacente. Por ejemplo, el **db_owner** rol fijo de base de datos tiene la **CONTROL DATABASE** permiso. Si el usuario tiene la **CONTROL DATABASE** permiso pero no es un miembro del rol, esta función informará correctamente que el usuario no es un miembro de la **db_owner** rol, aunque el usuario tiene el mismo permisos.  
  
## <a name="related-functions"></a>Funciones relacionadas  
 Para determinar si el usuario actual es miembro del grupo de Windows especificado o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rol de base de datos, utilice [IS_MEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-member-transact-sql.md). Para determinar si un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión es miembro de un rol de servidor, use [IS_SRVROLEMEMBER &#40; Transact-SQL &#41; ](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Se necesita el permiso VIEW DEFINITION en el rol de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se indica si el usuario actual es miembro del rol fijo de base de datos `db_datareader`.  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear rol &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [ELIMINAR rol &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [Crear rol de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [QUITAR el rol de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40; Transact-SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
