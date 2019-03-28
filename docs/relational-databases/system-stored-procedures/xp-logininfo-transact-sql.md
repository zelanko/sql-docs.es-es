---
title: xp_logininfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 5c214c8b061e2530c4dcf4b178b6028cbdca01fa
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530027"
---
# <a name="xplogininfo-transact-sql"></a>xp_logininfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre usuarios y grupos de Windows.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @acctname = ] 'account_name'` Es el nombre de un usuario de Windows o grupo que se le concedido acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *account_name* es **sysname**, su valor predeterminado es null. Si *account_name* no se especifica, todos los grupos de Windows y los usuarios de Windows que se han explícitamente permiso de inicio de sesión se notifican. *account_name* debe ser un nombre completo. Por ejemplo, 'ADVWKS4\macraes' o 'BUILTIN\Administrators'.  
  
 **'all'** | **"members"**  
 Especifica si se presenta información de todas las rutas de acceso a permisos de la cuenta o si se presenta información de los miembros del grupo de Windows. **@option** es **varchar (10)**, su valor predeterminado es null. A menos que **todas** se especifica, se muestra solo la primera ruta de permisos.  
  
`[ @privilege = ] variable_name` Es un parámetro de salida que devuelve el nivel de privilegio de la cuenta de Windows especificada. *variable_name* es **varchar (10)**, su valor predeterminado es 'Not wanted'. El nivel de privilegio devuelto es **usuario**, **admin**, o **null**.  
  
 OUTPUT  
 Cuando se especifica, coloca *variable_name* en el parámetro de salida.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre de cuenta**|**sysname**|Nombre completo de la cuenta de Windows.|  
|**Tipo**|**char(8)**|Tipo de cuenta de Windows. Los valores válidos son **usuario** o **grupo**.|  
|**privilege**|**char(9)**|Privilegio de acceso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los valores válidos son **admin**, **usuario**, o **null**.|  
|**nombre de inicio de sesión asignado**|**sysname**|Cuentas de usuario que tienen privilegio de usuario, **asigna el nombre de inicio de sesión** muestra el nombre de inicio de sesión asignado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta usar al iniciar sesión con esta cuenta mediante el uso de las reglas de asociación con el nombre de dominio agregado antes.|  
|**ruta de acceso de permiso**|**sysname**|Pertenencia al grupo que permite que la cuenta tenga acceso.|  
  
## <a name="remarks"></a>Comentarios  
 Si *account_name* se especifica, **xp_logininfo** notifica el nivel de privilegios más alto del grupo o usuario de Windows especificado. Si un usuario de Windows tiene acceso como administrador del sistema y como usuario del dominio, se le notificará como administrador del sistema. Si el usuario es miembro de varios grupos de Windows del mismo nivel de privilegio, solo se le notificará en el grupo al que se concediera primero acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si *account_name* es un usuario de Windows o grupo que no está asociado con válido un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, se devuelve un conjunto de resultados vacío. Si *account_name* no se puede identificar como un usuario válido de Windows o un grupo, se devuelve un mensaje de error.  
  
 Si *account_name* y **todas** son especificado, se devuelven todas las rutas de permisos para el usuario de Windows o grupo. Si *account_name* es un miembro de varios grupos, que ha concedido acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se devuelven varias filas. El **admin** se devuelven las filas del privilegio antes el **usuario** filas del privilegio y, dentro de un privilegio de nivel de filas devueltas en el orden en que el correspondiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se crearon inicios de sesión.  
  
 Si *account_name* y **miembros** son especificado, se devuelve una lista de los miembros del siguiente nivel del grupo. Si *account_name* es un grupo local, la lista puede incluir usuarios locales, los usuarios del dominio y grupos. Si *account_name* es una cuenta de dominio, la lista se compone de los usuarios del dominio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe conectarse al controlador de dominio para recuperar la información de pertenencia a grupos. Si el servidor no puede contactar con el controlador de dominio, no se obtendrá ninguna información.  
  
 **xp_logininfo** sólo devuelve información de grupos globales de Active Directory, los grupos universales no.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia a la **sysadmin** fijo de servidor o la pertenencia a la **pública** rol fijo de base de datos en el **maestro** base de datos con permiso de ejecución.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra información sobre la `BUILTIN\Administrators` grupo de Windows.  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
