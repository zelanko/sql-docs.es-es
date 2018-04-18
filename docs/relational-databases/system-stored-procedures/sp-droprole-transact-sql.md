---
title: sp_droprole (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff5636fc34877344b28f0309359b49baf7a83b32
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un rol de base de datos de la base de datos actual.  
  
> [!IMPORTANT]  
>  En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_droprole** ha sido reemplazado por la instrucción DROP ROLE. **sp_droprole** sólo se incluye por compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y podrían no admitirse en una versión futura.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***rol***'**  
 Es el nombre del rol de base de datos que se va a quitar de la base de datos actual. *rol* es un **sysname**, no tiene ningún valor predeterminado. *rol* ya debe existir en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Roles de base de datos solo se pueden quitar con **sp_droprole**.  
  
 No se puede quitar un rol de base de datos que tenga miembros. Todos los miembros de un rol de base de datos deben eliminarse previamente para poder quitar el rol de base de datos. Para quitar usuarios de un rol, utilice **sp_droprolemember**. Si los usuarios siguen siendo miembros del rol, **sp_droprole** muestra dichos miembros.  
  
 Roles fijos y los **público** no se puede quitar el rol.  
  
 Tampoco se puede quitar un rol que sea propietario de algún elemento protegible. Para poder quitar un rol de aplicación que posea elementos protegibles, primero debe transferir la propiedad de esos elementos o quitarlos. Use ALTER AUTHORIZATION para cambiar el propietario de los objetos que no se deban quitar.  
  
 **sp_droprole** no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL para el rol.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita el rol de aplicación `Sales`.  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_dropapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
