---
title: sp_helpsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 618ec7d83ab8abce8cf201cb0b59033b808178c0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533497"
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
`[ @srvrolename = ] 'role'` Es el nombre del rol fijo de servidor. *rol* es **sysname**, su valor predeterminado es null. Si *rol*no se especifica, el conjunto de resultados incluye información acerca de todos los roles fijos de servidor.  
  
 *rol* puede ser cualquiera de los siguientes valores.  
  
|Rol fijo de servidor|Descripción|  
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
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|Nombre del rol de servidor|  
|MemberName|**sysname**|Nombre de un miembro de ServerRole|  
|MemberSID|**varbinary(85)**|Identificador de seguridad de MemberName|  
  
## <a name="remarks"></a>Comentarios  
 Utilice sp_helprolemember para mostrar a los miembros de un rol de base de datos.  
  
 Todos los inicios de sesión están miembro del público. sp_helpsrvrolemember no reconoce el rol público porque, internamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no implementa pública como un rol.  
  
 Para agregar o quitadas miembros de los roles de servidor, consulte [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 sp_helpsrvrolemember no tiene un rol de servidor definido por el usuario como argumento. Para determinar los miembros del rol de servidor definido por el usuario, vea los ejemplos de [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
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
  
  
