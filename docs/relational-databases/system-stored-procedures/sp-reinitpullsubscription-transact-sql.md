---
title: sp_reinitpullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitpullsubscription_TSQL
- sp_reinitpullsubscription
helpviewer_keywords:
- sp_reinitpullsubscription
ms.assetid: 7d9abe49-ce92-47f3-82c9-aea749518c91
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1389e76d4e679a3ee16c548bf752d5668dfa48b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075674"
---
# <a name="spreinitpullsubscription-transact-sql"></a>sp_reinitpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca una suscripción transaccional de extracción o anónima para reinicializarla la próxima vez que se ejecute el Agente de distribución. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones de extracción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_reinitpullsubscription [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es all, que marca todas las suscripciones para reinicialización.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_reinitpullsubscription** se utiliza en la replicación transaccional.  
  
 **sp_reinitpullsubscription** no se admite para la replicación transaccional punto a punto.  
  
 **sp_reinitpullsubscription** pueden llamarse desde el suscriptor para reinicializar la suscripción, durante la próxima ejecución del agente de distribución.  
  
 Las suscripciones a publicaciones creadas con un valor de **false** para **@immediate_sync** no pueden reinicializarse desde el suscriptor.  
  
 Puede reinicializar una suscripción de extracción ejecutando **sp_reinitpullsubscription** en el suscriptor o **sp_reinitsubscription** en el publicador.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_reinitpullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitpullsubscriptio_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_reinitpullsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
