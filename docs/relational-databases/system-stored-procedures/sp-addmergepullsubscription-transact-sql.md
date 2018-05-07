---
title: sp_addmergepullsubscription (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_addmergepullsubscription_TSQL
- sp_addmergepullsubscription
helpviewer_keywords:
- sp_addmergepullsubscription
ms.assetid: d63909a0-8ea7-4734-9ce8-8204d936a3e4
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6d02490784dbbae3dba91aab940257300b4445eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es el nombre del servidor local. El publicador debe ser un servidor válido.  
  
 [  **@publisher_db =**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null.  
  
 [  **@subscriber_type=**] **'***subscriber_type***'**  
 Es el tipo de suscriptor. *propiedad subscriber_type* es **nvarchar (15)** y puede ser **global**, **local** o **anónimo**. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, las suscripciones locales se conocen como las suscripciones de cliente y suscripciones globales se conocen como suscripciones de servidor.  
  
 [  **@subscription_priority=**] *subscription_priority*  
 Es la prioridad de la suscripción. *subscription_priority*es **real**, su valor predeterminado es null. Para las suscripciones locales y anónimas, la prioridad es **0,0**. La prioridad la utiliza el solucionador predeterminado para elegir un ganador cuando se detectan conflictos. Para los suscriptores globales, la prioridad de la suscripción debe ser menor que 100, que es la prioridad del publicador.  
  
 [  **@sync_type=**] **'***sync_type***'**  
 Es el tipo de sincronización de suscripción. *sync_type*es **nvarchar (15)**, su valor predeterminado es **automática**. Puede ser **automática** o **ninguno**. Si **automática**, el esquema y los datos iniciales de las tablas publicadas se transfieren primero al suscriptor. Si **ninguno**, se supone el suscriptor ya tiene el esquema y los datos iniciales de las tablas publicadas. Las tablas y los datos del sistema se transfieren siempre.  
  
> [!NOTE]  
>  No se recomienda especificar un valor de **ninguno**.  
  
 [  **@description=**] **'***descripción***'**  
 Es una breve descripción de esta suscripción de extracción. *descripción*es **nvarchar (255)**, su valor predeterminado es null. Este valor se muestra el Monitor de replicación en el **Nombre_descriptivo** columna, que se puede usar para ordenar las suscripciones para una publicación supervisada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergepullsubscription** se usa para la replicación de mezcla.  
  
 Si usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente para sincronizar la suscripción, el [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) se debe ejecutar el procedimiento almacenado en el suscriptor para crear un agente y el trabajo se sincronicen con la publicación.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergepullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_1.sql)]  
  
 [!code-sql[HowTo#sp_addmergepullsub_websync_anon](../../relational-databases/replication/codesnippet/tsql/sp-addmergepullsubscript_0_2.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addmergepullsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción de extracción](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
