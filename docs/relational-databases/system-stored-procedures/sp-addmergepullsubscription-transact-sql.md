---
title: sp_addmergepullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98d31c0d4895573059104d43a1ebddd879ba1967
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52813127"
---
# <a name="spaddmergepullsubscription-transact-sql"></a>sp_addmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega una suscripción de extracción a una publicación de combinación. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergepullsubscription [ @publication= ] 'publication'   
    [ , [ @publisher= ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @subscriber_type= ] 'subscriber_type' ]   
    [ , [ @subscription_priority= ] subscription_priority ]   
    [ , [ @sync_type= ] 'sync_type' ]   
    [ , [ @description= ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'**_publicación_**'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher=**] **'**_publisher_**'**  
 Es el nombre del publicador. *Publicador* es **sysname**, su valor predeterminado es el nombre del servidor local. El publicador debe ser un servidor válido.  
  
 [  **@publisher_db =**] **'**_publisher_db_**'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_type=**] **'**_subscriber_type_**'**  
 Es el tipo de suscriptor. *propiedad subscriber_type* es **nvarchar (15)** y puede ser **global**, **local** o **anónimo**. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, las suscripciones locales se conocen como las suscripciones de cliente y se conocen las suscripciones globales como suscripciones de servidor.  
  
 [  **@subscription_priority=**] *subscription_priority*  
 Es la prioridad de la suscripción. *subscription_priority*es **real**, su valor predeterminado es null. Para las suscripciones locales y anónimas, la prioridad es **0.0**. La prioridad la utiliza el solucionador predeterminado para elegir un ganador cuando se detectan conflictos. Para los suscriptores globales, la prioridad de la suscripción debe ser menor que 100, que es la prioridad del publicador.  
  
 [  **@sync_type=**] **'**_sync_type_**'**  
 Es el tipo de sincronización de suscripción. *sync_type*es **nvarchar (15)**, su valor predeterminado es **automática**. Puede ser **automática** o **ninguno**. Si **automática**, el esquema y los datos iniciales de las tablas publicadas se transfieren primero al suscriptor. Si **ninguno**, se supone que el suscriptor ya tiene el esquema y los datos iniciales de las tablas publicadas. Las tablas y los datos del sistema se transfieren siempre.  
  
> [!NOTE]  
>  No se recomienda especificar un valor de **ninguno**.  
  
 [  **@description=**] **'**_descripción_**'**  
 Es una breve descripción de esta suscripción de extracción. *descripción*es **nvarchar (255)**, su valor predeterminado es null. Este valor se muestra el Monitor de replicación en el **Nombre_descriptivo** columna, que puede usarse para ordenar las suscripciones en una publicación supervisada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergepullsubscription** se usa para la replicación de mezcla.  
  
 Si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente para sincronizar la suscripción, el [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) se debe ejecutar el procedimiento almacenado en el suscriptor para crear un agente y trabajo para sincronizarlo con la publicación.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addmergepullsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
