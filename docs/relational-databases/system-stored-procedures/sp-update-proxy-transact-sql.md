---
title: sp_update_proxy (Transact-SQL) | Documentos de Microsoft
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
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 072c36097eb465fa43a785c59d4b0ef73d6d351f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259815"
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un proxy existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id**=] *Id.*  
 Número de identificación del proxy que se va a cambiar. El *proxy_id* es **int**, su valor predeterminado es null.  
  
 [ **@proxy_name**=] **'***proxy_name***'**  
 Nombre del proxy que se va a cambiar. El *proxy_name* es **sysname**, su valor predeterminado es null.  
  
 [ **@credential_name** =] **'***credential_name***'**  
 Nombre de la nueva credencial para el proxy. El *credential_name* es **sysname**, su valor predeterminado es null. Cualquier *credential_name* o *credential_id* se puede especificar.  
  
 [ **@credential_id** =] *credential_id*  
 Número de identificación de la nueva credencial para el proxy. El *credential_id* es **int**, su valor predeterminado es null. Cualquier *credential_name* o *credential_id* se puede especificar.  
  
 [ **@new_name**=] **'***new_name***'**  
 Nuevo nombre del proxy. El *new_name* es **sysname**, su valor predeterminado es null. Si se proporciona, el procedimiento cambia el nombre del proxy para *new_name*. Si este argumento es NULL, el nombre del proxy no varía.  
  
 [ **@enabled** =] *is_enabled*  
 Es si el proxy está habilitado. El *is_enabled* marca es **tinyint**, su valor predeterminado es null. Cuando *is_enabled* es **0**, el proxy no está habilitado y no puede usar un paso de trabajo. Si este argumento es NULL, el estado del proxy no varía.  
  
 [ **@description**=] **'***descripción***'**  
 Nueva descripción del proxy. El *descripción* es **nvarchar (512)**, su valor predeterminado es null. Si este argumento es NULL, la descripción del proxy no varía.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Cualquier **@proxy_name** o **@proxy_id** debe especificarse. Si se especifican los dos argumentos, deben hacer referencia al mismo proxy; de lo contrario, el procedimiento almacenado genera un error.  
  
 Cualquier **@credential_name** o **@credential_id** debe especificarse para cambiar las credenciales del proxy. Si se especifican los dos argumentos, deben hacer referencia a la misma credencial; de lo contrario, el procedimiento almacenado genera un error.  
  
 Este procedimiento cambia el proxy, pero no cambia el acceso al proxy. Para cambiar el acceso a un servidor proxy, use **sp_grant_login_to_proxy** y **sp_revoke_login_from_proxy**.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de seguridad puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se establece el valor habilitado para el `Catalog application proxy` en `0`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del Agente SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [Implementar la seguridad del Agente SQL Server](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
