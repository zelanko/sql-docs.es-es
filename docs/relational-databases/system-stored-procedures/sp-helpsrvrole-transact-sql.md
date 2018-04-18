---
title: sp_helpsrvrole (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
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
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9427712cb6a55ae5b42962b8a117d11db1c5268
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de los roles fijos de servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@srvrolename=** ] **'***rol***'**  
 Es el nombre del rol fijo de servidor. *rol* es **sysname**, su valor predeterminado es null. *rol* puede ser uno de los siguientes valores.  
  
|Rol fijo de servidor|Description|  
|-----------------------|-----------------|  
|sysadmin|Administradores del sistema|  
|securityadmin|Administradores de seguridad|  
|serveradmin|Administradores de servidor|  
|setupadmin|Administradores de instalación|  
|processadmin|Administradores de proceso|  
|diskadmin|Administradores de disco|  
|dbcreator|Creadores de bases de datos|  
|bulkadmin|Puede ejecutar instrucciones BULK INSERT|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|Nombre del rol de servidor|  
|Description|**sysname**|Descripción de ServerRole|  
  
## <a name="remarks"></a>Comentarios  
 Los roles fijos de servidor están definidos en el nivel de servidor y tienen permisos para ejecutar actividades administrativas específicas en el servidor. Los roles fijos de servidor no se pueden agregar, quitar ni cambiar.  
  
 Para agregar o quitar miembros de roles de servidor, consulte [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Todos los inicios de sesión están miembro del público. sp_helpsrvrole no reconoce la función public porque, internamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no implementa públicos como un rol.  
  
 sp_helpsrvrole no tiene un rol de servidor definidos por el usuario como un argumento. Para obtener una lista de los roles de servidor definidos por el usuario, vea los ejemplos de [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-the-fixed-server-roles"></a>A. Enumerar los roles fijos de servidor  
 En el siguiente ejemplo se devuelve la lista de los roles fijos de servidor.  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>B. Lista de roles de servidor fijos y definidos por el usuario  
 La siguiente consulta devuelve una lista tanto de los roles fijos de servidor como de los definidos por el usuario.  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>C. Devolver una descripción de un rol fijo de servidor  
 La siguiente consulta devuelve el nombre y la descripción de los roles fijos de servidor `diskadmin`.  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
