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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d9a581803d232f704dd27592a354c6331660ac03
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751706"
---
# <a name="sp_reinitpullsubscription-transact-sql"></a>sp_reinitpullsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Marca una suscripción transaccional de extracción o anónima para reinicializarla la próxima vez que se ejecute el Agente de distribución. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones de extracción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_reinitpullsubscription [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos del publicador. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname y su**valor predeterminado es All, que marca todas las suscripciones para reinicializarlas.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_reinitpullsubscription** se utiliza en la replicación transaccional.  
  
 **sp_reinitpullsubscription** no se admite para la replicación transaccional punto a punto.  
  
 se puede llamar a **sp_reinitpullsubscription** desde el suscriptor para reinicializar la suscripción, durante la siguiente ejecución de la agente de distribución.  
  
 Las suscripciones a publicaciones creadas con un valor de **false** para ** \@ immediate_sync** no se pueden reinicializar desde el suscriptor.  
  
 Puede reinicializar una suscripción de extracción ejecutando **sp_reinitpullsubscription** en el suscriptor o **Sp_reinitsubscription** en el publicador.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_reinitpullsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitpullsubscriptio_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_reinitpullsubscription**.  
  
## <a name="see-also"></a>Consulte también  
 [Reinicializar una suscripción](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
