---
title: sp_grant_login_to_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
manager: jrothj
ms.openlocfilehash: 81aeb41fdf7c8c17d5035347d384e7175bbd891b
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822670"
---
# <a name="spgrantlogintoproxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede acceso a una entidad de seguridad al proxy.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login_name = ] 'login_name'` El nombre de inicio de sesión para conceder acceso a. El *login_name* es **nvarchar (256)** , su valor predeterminado es null. Uno de **@login_name** , **@fixed_server_role** , o **@msdb_role** debe especificarse, o se produce un error en el procedimiento almacenado.  
  
`[ @fixed_server_role = ] 'fixed_server_role'` El rol fijo de servidor para conceder acceso a. El *fixed_server_role* es **nvarchar (256)** , su valor predeterminado es null. Uno de **@login_name** , **@fixed_server_role** , o **@msdb_role** debe especificarse, o se produce un error en el procedimiento almacenado.  
  
`[ @msdb_role = ] 'msdb_role'` El rol de base de datos en el **msdb** para conceder acceso a base de datos. El *msdb_role* es **nvarchar (256)** , su valor predeterminado es null. Uno de **@login_name** , **@fixed_server_role** , o **@msdb_role** debe especificarse, o se produce un error en el procedimiento almacenado.  
  
`[ @proxy_id = ] id` El identificador para el proxy conceder acceso. El *id* es **int**, su valor predeterminado es null. Uno de **@proxy_id** o **@proxy_name** debe especificarse, o se produce un error en el procedimiento almacenado.  
  
`[ @proxy_name = ] 'proxy_name'` El nombre del servidor proxy para conceder acceso. El *proxy_name* es **nvarchar (256)** , su valor predeterminado es null. Uno de **@proxy_id** o **@proxy_name** debe especificarse, o se produce un error en el procedimiento almacenado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_grant_login_to_proxy** se debe ejecutar desde la **msdb** base de datos.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** puede ejecutar el rol fijo de servidor **sp_grant_login_to_proxy**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se permite el inicio de sesión `adventure-works\terrid` para usar el proxy `Catalog application proxy`.  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
