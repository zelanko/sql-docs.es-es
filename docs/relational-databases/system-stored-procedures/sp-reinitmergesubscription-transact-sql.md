---
title: sp_reinitmergesubscription (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_reinitmergesubscription_TSQL
- sp_reinitmergesubscription
helpviewer_keywords:
- sp_reinitmergesubscription
ms.assetid: 249a4048-e885-48e0-a92a-6577f59de751
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: be5906700c4a1ced7b6977923bfa5d63e4678401
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spreinitmergesubscription-transact-sql"></a>sp_reinitmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca una suscripción de mezcla para reinicializarla la próxima vez que se ejecute el Agente de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
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
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **todos los**.  
  
 [  **@subscriber =** ] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es **todos los**.  
  
 [  **@subscriber_db =** ] **'***subscriber_db***'**  
 Es el nombre de la base de datos del suscriptor. *subscriber_db* es **sysname**, su valor predeterminado es **todos los**.  
  
 [  **@upload_first =** ] **'***upload_first***'**  
 Especifica si se cargan los cambios del suscriptor antes de que se reinicialice la suscripción. *upload_first* es **nvarchar (5)**, con un valor predeterminado es FALSE. Si **true**, cambios se cargan antes de reinicializar la suscripción. Si **false**, no se cargan los cambios.  
  
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
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos puede ejecutar **sp_reinitmergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Reinicializar suscripciones](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
