---
title: sp_revoke_login_from_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0aad616275d635ac32d6e81dbc5321db0db58b34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019941"
---
# <a name="sprevokeloginfromproxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita el acceso a un proxy correspondiente a una entidad de seguridad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` El nombre de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión, rol de servidor o **msdb** rol de base de datos para quitar el acceso. *nombre* es **nvarchar (256)** no tiene ningún valor predeterminado.  
  
`[ @proxy_id = ] id` El identificador del proxy para quitar el acceso. Cualquier *id* o *proxy_name* debe especificarse, pero no se pueden especificar ambos. El *id* es **int**, su valor predeterminado es null.  
  
`[ @proxy_name = ] 'proxy_name'` El nombre del servidor proxy para quitar el acceso. Cualquier *id* o *proxy_name* debe especificarse, pero no se pueden especificar ambos. El *proxy_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Los trabajos propiedad del inicio de sesión que hace referencia a este proxy no podrán ejecutarse.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, un usuario debe ser miembro del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo revoca el acceso del inicio de sesión `terrid` al proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_help_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
