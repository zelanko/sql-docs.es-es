---
title: sp_addremotelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e23684e04d8e49d1a6456185f94ad74b71b1604c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537932"
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo identificador de inicio de sesión remoto en el servidor local. Esto permite a los servidores remotos conectarse y ejecutar llamadas a procedimientos remotos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Utilice servidores vinculados y procedimientos almacenados de servidores vinculados en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @remoteserver **=** ] **'**_remoteserver_**'**  
 Es el nombre del servidor remoto al que se aplica el inicio de sesión remoto. *remoteserver* es **sysname**, no tiene ningún valor predeterminado. Si solo *remoteserver* se especifica, todos los usuarios en *remoteserver* se asignan a inicios de sesión existentes del mismo nombre en el servidor local. El servidor debe ser un servidor conocido por el servidor local. Esto se agrega mediante sp_addserver. Cuando los usuarios en *remoteserver* conectarse al servidor local que se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar un procedimiento almacenado remoto, conectan con el inicio de sesión local que coincide con su propio inicio de sesión en *remoteserver* . *remoteserver* es el servidor que inicia la llamada a procedimiento remoto.  
  
 [ @loginame **=** ] **'**_inicio de sesión_**'**  
 Es el identificador de inicio de sesión del usuario en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* es de tipo **sysname** y su valor predeterminado es NULL. *inicio de sesión*ya debe existir en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si *inicio de sesión* se especifica, todos los usuarios en *remoteserver* se asignan a ese inicio de sesión local específico. Cuando los usuarios en *remoteserver* conectarse a la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar un procedimiento almacenado remoto, conectan con *inicio de sesión*.  
  
 [ @remotename **=** ] **'**_remote_name_**'**  
 Es el identificador de inicio de sesión del usuario en el servidor remoto. *remote_name* es **sysname**, su valor predeterminado es null. *remote_name* debe existir en *remoteserver*. Si *remote_name* se especifica, el usuario específico *remote_name* se asigna a *inicio de sesión* en el servidor local. Cuando *remote_name* en *remoteserver* se conecta a la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar un procedimiento almacenado remoto, se conecta como *inicio de sesión*. El identificador de inicio de sesión de *remote_name* puede ser diferente del identificador de inicio de sesión en el servidor remoto, *inicio de sesión*.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Para ejecutar consultas distribuidas, utilice sp_addlinkedsrvlogin.  
  
 sp_addremotelogin no se puede usar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de sysadmin y securityadmin roles fijos de servidor pueden ejecutar sp_addremotelogin.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-mapping-one-to-one"></a>A. Asignar uno a uno  
 En el siguiente ejemplo se asignan nombres remotos a nombres locales cuando el servidor remoto `ACCOUNTS` y el servidor local tienen los mismos inicios de sesión de usuario.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>b. Asignar varios a uno  
 En el siguiente ejemplo se crea una entrada que asigna todos los usuarios del servidor remoto `ACCOUNTS` al Id. de inicio de sesión local `Albert`.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. Usar una asignación uno a uno explícita  
 En el siguiente ejemplo se asigna un inicio de sesión remoto desde el usuario remoto `Chris` en el servidor remoto `ACCOUNTS` al usuario local `salesmgr`.  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
