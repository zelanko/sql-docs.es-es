---
title: sp_reinitmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ee55dcde7ce098ad9d2c07ba93cefa45216e205
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633993"
---
# <a name="spreinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca una suscripción de mezcla para reinicializarla la próxima vez que se ejecute el Agente de mezcla. Este procedimiento almacenado se ejecuta en la base de datos de publicación del publicador.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_reinitmergesubscription [ [ @publication = ] 'publication'  
    [ , [ @subscriber = ] 'subscriber'  
    [ , [ @subscriber_db = ] 'subscriber_db'  
    [ , [ @upload_first = ] 'upload_first'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **todas**.  
  
 [  **@subscriber =** ] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es **todas**.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 Es el nombre de la base de datos del suscriptor. *subscriber_db* es **sysname**, su valor predeterminado es **todas**.  
  
 [  **@upload_first =** ] **'***upload_first***'**  
 Especifica si se cargan los cambios del suscriptor antes de que se reinicialice la suscripción. *upload_first* es **nvarchar (5)**, su valor predeterminado es False. Si **true**, los cambios se cargan antes de reinicializar la suscripción. Si **false**, no se cargan los cambios.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_reinitmergesubscription** se utiliza en la replicación de mezcla.  
  
 **sp_reinitmergesubscription** pueden llamarse desde el publicador para reinicializar las suscripciones de mezcla. También se recomienda volver a ejecutar el Agente de instantáneas.  
  
 Si se agrega, quita o modifica un filtro con parámetros, los cambios pendientes en el suscriptor no se pueden cargar en el publicador durante la reinicialización. Si desea cargar los cambios pendientes, sincronice todas las suscripciones antes de cambiar el filtro.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_reinitmergepushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_1.sql)]  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_reinitmergepushsubwithupload](../../relational-databases/replication/codesnippet/tsql/sp-reinitmergesubscripti_2.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_reinitmergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
