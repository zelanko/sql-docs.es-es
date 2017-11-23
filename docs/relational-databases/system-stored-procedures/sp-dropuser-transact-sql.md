---
title: sp_dropuser (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropuser
- sp_dropuser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: cea8bee162f25ad22448007026d90ce0835c568e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un usuario de base de datos de la base de datos actual. **sp_dropuser** proporciona compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) en su lugar.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name_in_db =**] **'***usuario***'**  
 Es el nombre del usuario que se va a quitar. *usuario* es un **sysname**, no tiene ningún valor predeterminado. *usuario* debe existir en la base de datos actual. Cuando especifique un inicio de sesión de Windows, utilice el nombre por el que se conoce ese inicio de sesión en la base de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropuser** ejecuta **sp_revokedbaccess** para quitar el usuario de la base de datos actual.  
  
 Use **sp_helpuser** para mostrar una lista de los nombres de usuario que se pueden quitar de la base de datos actual.  
  
 Cuando se quita un usuario de base de datos, también se quitan los alias que el usuario tuviera. Si el usuario posee un esquema vacío con su mismo nombre, se eliminará también el esquema. Si el usuario posee otros elementos protegibles en la base de datos, no se eliminará el usuario. La propiedad de los objetos debe transferirse primero a otra entidad de seguridad. Para obtener más información, vea [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md). Al quitar un usuario de la base de datos se quitan automáticamente los permisos que tiene asociados y, también, se quita el usuario de todos los roles de los que es miembro.  
  
 **sp_dropuser** no se puede usar para quitar el propietario de la base de datos (**dbo**) **INFORMATION_SCHEMA** a los usuarios, o la **invitado** usuario desde el  **maestro** o **tempdb** bases de datos. En las bases de datos ajenos al sistema, `EXEC sp_dropuser 'guest'` revocará el permiso CONNECT al usuario **invitado**. Pero no se quitará al usuario.  
  
 **sp_dropuser** no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY USER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se quita el usuario `Albert` de la base de datos actual.  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguridad almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [Eliminar usuario &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
