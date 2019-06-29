---
title: sp_dropsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropsrvrolemember
- sp_dropsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropsrvrolemember
ms.assetid: 7be99181-d221-49d0-9cb2-c930d8c044a0
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 2624ed4800a247b0847adc5839346758aa50f140
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463565"
---
# <a name="spdropsrvrolemember-transact-sql"></a>sp_dropsrvrolemember (Transact-SQL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Quita un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un usuario o grupo de Windows de un rol fijo de servidor.

> [!IMPORTANT]
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER SERVER ROLE](../../t-sql/statements/alter-server-role-transact-sql.md) en su lugar.

![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxis

```
sp_dropsrvrolemember [ @loginame = ] 'login' , [ @rolename = ] 'role'  
```

## <a name="arguments"></a>Argumentos

**[ @loginame =]** '_inicio de sesión_'  
Es el nombre del inicio de sesión que se va a quitar del rol fijo de servidor. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* debe existir.  

**[ @rolename = ]** '_role_'  
Es el nombre de un rol de servidor. *rol* es **sysname**, su valor predeterminado es null. *función* debe ser uno de los siguientes valores:  

-   sysadmin  
  
-   securityadmin  
  
-   serveradmin  
  
-   setupadmin  
  
-   processadmin  
  
-   diskadmin  
  
-   dbcreator  
  
-   bulkadmin 
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Sp_dropsrvrolemember solo puede usarse para quitar un inicio de sesión de un rol fijo de servidor. Utilice sp_droprolemember para quitar a un miembro de un rol de base de datos.  
  
 No se puede quitar el inicio de sesión de sa de ningún rol fijo de servidor.  
  
 no se puede ejecutar sp_dropsrvrolemember dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijada de servidor, o ambos permisos ALTER ANY LOGIN en el servidor y la pertenencia al rol desde el que se va a quitar el miembro de sysadmin.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita el inicio de sesión `JackO` del rol fijo de servidor `sysadmin`.  
  
```sql
EXEC sp_dropsrvrolemember 'JackO', 'sysadmin';  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [DROP SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
