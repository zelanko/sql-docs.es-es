---
title: sp_helpsrvrolemember (Transact-SQL) | Documentos de Microsoft
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
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d4c800464cf0da918e748ba6b6c9d1ffc4c093a0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de los miembros de un rol fijo de servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@srvrolename =** ] **'***rol***'**  
 Es el nombre de un rol fijo de servidor. *rol* es **sysname**, su valor predeterminado es null. Si *rol*no se especifica, el conjunto de resultados incluye información acerca de todos los roles fijos de servidor.  
  
 *rol* puede ser cualquiera de los siguientes valores.  
  
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
|MemberName|**sysname**|Nombre de un miembro de ServerRole|  
|MemberSID|**varbinary(85)**|Identificador de seguridad de MemberName|  
  
## <a name="remarks"></a>Comentarios  
 Utilice sp_helprolemember para mostrar a los miembros de un rol de base de datos.  
  
 Todos los inicios de sesión están miembro del público. sp_helpsrvrolemember no reconoce la función public porque, internamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no implementa públicos como un rol.  
  
 Para agregar o quitar miembros de roles de servidor, consulte [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 sp_helpsrvrolemember no tiene un rol de servidor definidos por el usuario como un argumento. Para determinar los miembros de un rol de servidor definidos por el usuario, vea los ejemplos de [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se enumeran los miembros del rol fijo de servidor `sysadmin`.  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
