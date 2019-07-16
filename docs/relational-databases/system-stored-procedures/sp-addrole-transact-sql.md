---
title: sp_addrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1711ec3941a5fced5ef9e0c32808d6153b673e2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030921"
---
# <a name="spaddrole-transact-sql"></a>sp_addrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un rol de base de datos nuevo en la base de datos actual.  
  
> [!IMPORTANT]
>  **sp_addrole** se incluye por compatibilidad con versiones anteriores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y podrían no admitirse en una versión futura. Use [CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'` Es el nombre del nuevo rol de base de datos. *rol* es un **sysname**, no tiene ningún valor predeterminado. *función* debe ser un identificador válido (ID) y no debe existir en la base de datos actual.  
  
`[ @ownername = ] 'owner'` Es el propietario del nuevo rol de base de datos. *propietario* es un **sysname**, su valor predeterminado es el usuario actual. *propietario* debe ser un usuario de base de datos o el rol de base de datos en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Los nombres de los roles de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden contener de 1 a 128 caracteres, incluidos letras, símbolos y números. Los nombres de roles de base de datos no pueden: contienen un carácter de barra diagonal inversa (\\), es nulo, o una cadena vacía ( **''** ).  
  
 Después de agregar un rol de base de datos, use [sp_addrolemember &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) agregar entidades a la función. Cuando se utilizan las instrucciones GRANT, DENY o REVOKE para aplicar permisos al rol de base de datos, los miembros de este rol heredan estos permisos como si se aplicaran directamente a sus cuentas.  
  
> [!NOTE]  
>  No se pueden crear roles de servidor nuevos. Los roles solo pueden crearse en las bases de datos.  
  
 **sp_addrole** no se puede usar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CREATE ROLE en la base de datos. Si crea un esquema, es necesario el permiso CREATE SCHEMA en la base de datos. Si *propietario* se especifica como un usuario o grupo, necesario el permiso IMPERSONATE sobre ese usuario o grupo. Si *propietario* se especifica como un rol, necesita el permiso de ALTER en ese rol o en un miembro de dicho rol. Si se especifica owner como rol de aplicación, es necesario el permiso ALTER en ese rol de aplicación.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se agrega un nuevo rol llamado `Managers` a la base de datos actual.  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
