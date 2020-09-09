---
description: sp_droprole (Transact-SQL)
title: sp_droprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6180676b4458a5f270f9ecab9bb35d2ed8a481c4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548149"
---
# <a name="sp_droprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Quita un rol de base de datos de la base de datos actual.  
  
> [!IMPORTANT]  
>  En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , **sp_droprole** se ha reemplazado por la instrucción DROP Role. **sp_droprole** solo se incluye para la compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y es posible que no se admita en una versión futura.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'` Es el nombre del rol de base de datos que se va a quitar de la base de datos actual. *role* es un **sysname**y no tiene ningún valor predeterminado. el *rol* ya debe existir en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Solo se pueden quitar roles de base de datos mediante **sp_droprole**.  
  
 No se puede quitar un rol de base de datos que tenga miembros. Todos los miembros de un rol de base de datos deben eliminarse previamente para poder quitar el rol de base de datos. Para quitar usuarios de un rol, use **sp_droprolemember**. Si los usuarios siguen siendo miembros del rol, **sp_droprole** los muestra.  
  
 Los roles fijos y el rol **Public** no se pueden quitar.  
  
 Tampoco se puede quitar un rol que sea propietario de algún elemento protegible. Para poder quitar un rol de aplicación que posea elementos protegibles, primero debe transferir la propiedad de esos elementos o quitarlos. Use ALTER AUTHORIZATION para cambiar el propietario de los objetos que no se deban quitar.  
  
 **sp_droprole** no se puede ejecutar en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
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
 [sp_dropapprole &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
