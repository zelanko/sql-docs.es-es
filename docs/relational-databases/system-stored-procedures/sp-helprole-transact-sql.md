---
title: sp_helprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprole_TSQL
- sp_helprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprole
ms.assetid: b023103f-ccf3-44e2-b418-4be9bdd49f4a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4caa5d8ab850c06aec62b84088463dc21bb40ea2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997497"
---
# <a name="sp_helprole-transact-sql"></a>sp_helprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de los roles de la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helprole [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`Es el nombre de un rol de la base de datos actual. *role* es de **tipo sysname y su**valor predeterminado es NULL. el *rol* debe existir en la base de datos actual. Si no se especifica *role* , se devuelve información acerca de todos los roles de la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**RoleName**|**sysname**|Nombre del rol en la base de datos actual.|  
|**RoleId**|**smallint**|IDENTIFICADOR de **RoleName**.|  
|**IsAppRole**|**int**|0 = **RoleName** no es un rol de aplicación.<br /><br /> 1 = **RoleName** es un rol de aplicación.|  
  
## <a name="remarks"></a>Observaciones  
 Para ver los permisos asociados con el rol, use **sp_helprotect**. Para ver los miembros de un rol de base de datos, use **sp_helprolemember**.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En la siguiente consulta se devuelven todos los roles de la base de datos actual.  
  
```  
EXEC sp_helprole  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [sp_addapprole &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [sp_addrole &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [sp_droprole &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [sp_helprolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [sp_helpsrvrolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
