---
title: sp_dropsubscriber (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_dropsubscriber_TSQL
- sp_dropsubscriber
helpviewer_keywords: sp_dropsubscriber
ms.assetid: 8c6eb282-81b5-4ec4-b691-aa061d9267dc
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85ee8e099e742db5f650a9eef15aab87880542e9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spdropsubscriber-transact-sql"></a>sp_dropsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita la designación de suscriptor de un servidor registrado. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Este procedimiento almacenado ha quedado desusado. Ya no es necesario registrar de forma explícita un suscriptor en el publicador.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropsubscriber [ @subscriber= ] 'subscriber'   
    [ , [ @reserved= ] 'reserved' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@subscriber=** ] **'***suscriptor***'**  
 Es el nombre del suscriptor que se va a quitar. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@reserved=** ] **'***reservada***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@ignore_distributor =** ] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropsubscriber** se utiliza en todos los tipos de replicación.  
  
 Este procedimiento almacenado quita el servidor **sub** opción y se quita la asignación de inicio de sesión remoto del administrador del sistema para **repl_subscriber**.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_dropsubscriber**.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar una suscripción de inserción](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Eliminar una suscripción de extracción](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addsubscriber &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
