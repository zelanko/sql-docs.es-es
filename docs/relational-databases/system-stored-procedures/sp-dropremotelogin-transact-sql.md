---
title: sp_dropremotelogin (Transact-SQL) | Documentos de Microsoft
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
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7f1262ade6b92cdcac57df0397e9f6c57ee47c23
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un inicio de sesión remoto asignado a un inicio de sesión local que se utiliza para ejecutar procedimientos almacenados remotos en el servidor local que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilice en su lugar servidores vinculados y procedimientos almacenados del servidor vinculado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@remoteserver =** ] **'***remoteserver***'**  
 Es el nombre del servidor remoto asignado al inicio de sesión remoto que se va a quitar. *remoteserver* es **sysname**, no tiene ningún valor predeterminado. *remoteserver* ya debe existir.  
  
 [ **@loginame =** ] **'***login***'**  
 Es el nombre de inicio de sesión opcional en el servidor local, asociado al servidor remoto. *login* es de tipo **sysname** y su valor predeterminado es NULL. *inicio de sesión* ya debe existir si se especifica.  
  
 [  **@remotename =** ] **'***remote_name***'**  
 Es el nombre opcional del inicio de sesión remoto asignado a *inicio de sesión* al iniciar sesión desde el servidor remoto. *remote_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Si solo *remoteserver* se especifica, se quitan todos los inicios de sesión remotos para ese servidor remoto desde el servidor local. Si *inicio de sesión* también está especificados, que todos los inicios de sesión de *remoteserver* inicio de sesión local asignado específicos que se quitan del servidor local. Si *remote_name* también se especifica, solo el inicio de sesión remoto de ese usuario remoto desde *remoteserver* se quita del servidor local.  
  
 Para agregar usuarios al servidor local, use **sp_addlogin**. Para quitar usuarios del servidor local, use **sp_droplogin**.  
  
 Los inicios de sesión remotos solo son necesarios cuando se usan versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0 y posteriores utilizan en su lugar inicios de sesión de servidores vinculados. Use **sp_addlinkedsrvlogin** y **sp_droplinkedsrvlogin** para agregar y quitar inicios de sesión de servidor vinculado.  
  
 **sp_dropremotelogin** no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** o **securityadmin** roles fijos de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. Quitar todos los inicios de sesión remotos de un servidor remoto  
 En el siguiente ejemplo se quita la entrada del servidor remoto `ACCOUNTS`, con lo que se quitan también todas las asignaciones entre inicios de sesión del servidor local e inicios de sesión remotos del servidor remoto.  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. Quitar una asignación de inicio de sesión  
 En el siguiente ejemplo se quita la entrada que asigna inicios de sesión remotos del servidor remoto `ACCOUNTS` al nombre de inicio de sesión local `Albert`.  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. Quitar un usuario remoto  
 En el siguiente ejemplo se quita el inicio de sesión remoto `Chris` del servidor remoto `ACCOUNTS`, asignado al inicio de sesión local `salesmgr`.  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
