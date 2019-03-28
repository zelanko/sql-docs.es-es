---
title: sp_dropmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergesubscription_TSQL
- sp_dropmergesubscription
helpviewer_keywords:
- sp_dropmergesubscription
ms.assetid: 34244ae6-bd98-4a6a-bbd3-85f50edfcdc0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b360eed1619317e7ca3092bc47da086c520bf04
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535557"
---
# <a name="spdropmergesubscription-transact-sql"></a>sp_dropmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una suscripción a una publicación de combinación y su Agente de mezcla asociado. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergesubscription [ [ @publication= ] 'publication' ]   
    [ , [ @subscriber= ] 'subscriber'    
    [ , [ @subscriber_db= ] 'subscriber_db' ]   
    [ , [ @subscription_type= ] 'subscription_type' ]   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de publicación. *publicación* es **sysname**, su valor predeterminado es null. La publicación debe existir y debe cumplir las normas de los identificadores.  
  
`[ @subscriber = ] 'subscriber'` Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es null.  
  
`[ @subscriber_db = ] 'subscriber_db'` Es el nombre de la base de datos de suscripción. *subscription_database*es **sysname**, su valor predeterminado es null.  
  
`[ @subscription_type = ] 'subscription_type'` Es el tipo de suscripción. *subscription_type*es **nvarchar (15)**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**all**|Suscripciones de inserción, de extracción y anónimas.|  
|**anonymous**|Suscripción anónima.|  
|**push**|Suscripción de inserción.|  
|**pull**|Suscripción de extracción.|  
|**ambos** (valor predeterminado)|Suscripción de inserción y de extracción.|  
  
`[ @ignore_distributor = ] ignore_distributor` Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es **bit**, su valor predeterminado es **0**. Este parámetro se puede utilizar para quitar una suscripción sin tener que realizar tareas de limpieza en el distribuidor. También es útil cuando ha sido necesario volver a instalar el distribuidor.  
  
`[ @reserved = ] reserved` está reservado para uso futuro. *reservado* es **bit**, su valor predeterminado es **0**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergesubscription** se utiliza en la replicación de mezcla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergesubscription_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_dropmergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar una suscripción de inserción](../../relational-databases/replication/delete-a-push-subscription.md)   
 [Eliminar una suscripción de extracción](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
