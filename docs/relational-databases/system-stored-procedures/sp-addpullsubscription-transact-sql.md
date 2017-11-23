---
title: sp_addpullsubscription (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
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
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords: sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b6c772cc91d922ceb8acd5c205c9b19dc67d50d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega una suscripción de extracción a una publicación de instantáneas o transaccional. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos donde se va a crear la suscripción de extracción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es null. *publisher_db* omite los publicadores de Oracle.  
  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 Especifica si hay un agente de distribución independiente para esta publicación. *independent_agent* es **nvarchar (5)**, con un valor predeterminado es TRUE. Si **true**, hay un agente de distribución independiente para esta publicación. Si **false**, hay un agente de distribución para cada pareja de base de datos de base de datos de suscriptor de publicador. *independent_agent* es una propiedad de la publicación y debe tener el mismo valor aquí y en el publicador.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 Es el tipo de suscripción. *subscription_type* es **nvarchar(9)**, su valor predeterminado es **anónimo**. Debe especificar un valor de **extracción** para *subscription_type*, a menos que desee crear una suscripción sin registrar la suscripción en el publicador. En este caso, debe especificar un valor de **anónimo**. Esto es necesario para los casos en los que no se puede establecer un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexión al publicador durante la configuración de la suscripción.  
  
 [  **@description=**] **'***descripción***'**  
 Es la descripción de la publicación. *descripción* es **nvarchar (100)**, su valor predeterminado es null.  
  
 [  **@update_mode=**] **'***update_mode***'**  
 Es el tipo de actualización. *update_mode* es **nvarchar (30)**, y puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**sólo lectura** (valor predeterminado)|La suscripción es de solo lectura. Los cambios en el suscriptor no se devuelven al publicador. Se debe utilizar cuando las actualizaciones no se realicen en el suscriptor.|  
|**Synctran**|Habilita la compatibilidad con las suscripciones de actualización inmediata.|  
|**tran en cola**|Permite la actualización en cola de la suscripción. Las modificaciones de los datos se realizan en el suscriptor, se almacenan en una cola y después se propagan al publicador.|  
|**conmutación por error**|Permite la actualización inmediata de las suscripciones con la actualización en cola como conmutación por error. Las modificaciones de los datos se pueden realizar en el suscriptor y propagarse inmediatamente al publicador. Si el publicador y el suscriptor no están conectados, las modificaciones de los datos realizadas en el suscriptor pueden almacenarse en una cola hasta que el suscriptor y el publicador vuelvan a conectarse.|  
|**en cola de conmutación por error**|Habilita la suscripción como una suscripción de actualización en cola con la capacidad de cambiar al modo de actualización inmediata. Las modificaciones de los datos se pueden realizar en el suscriptor y almacenarse en una cola hasta que se establezca una conexión entre el suscriptor y el publicador. Cuando se establece una conexión continua, el modo de actualización puede cambiar a actualización inmediata. *No se admite en publicadores de Oracle*.|  
  
 [  **@immediate_sync =**] *immediate_sync*  
 Indica si los archivos de sincronización se crean, o se vuelven a crear, cada vez que se ejecuta el agente de instantáneas. *immediate_sync* es **bits** con un valor predeterminado es 1 y debe establecerse en el mismo valor que *immediate_sync* en **sp_addpublication**. *immediate_sync* es una propiedad de la publicación y debe tener el mismo valor aquí y en el publicador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addpullsubscription** se utiliza en la replicación de instantáneas y transaccional.  
  
> [!IMPORTANT]  
>  En el caso de las suscripciones de actualización en cola, utilice la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las conexiones a los suscriptores y especifique otra cuenta para la conexión a cada suscriptor. Al crear una suscripción de extracción que admita la actualización en cola, la replicación siempre establece el uso de la autenticación de Windows en la conexión (en suscripciones de extracción, la replicación no puede tener acceso a metadatos en el suscriptor con autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). En este caso, debe ejecutar [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) para cambiar la conexión para utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación después de configurar la suscripción.  
  
 Si el [MSreplication_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) la tabla no existe en el suscriptor, **sp_addpullsubscription** lo crea. También agrega una fila a la [MSreplication_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabla. Para las suscripciones de extracción, [sp_addsubscription &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) primero se debe llamar en el publicador.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addpullsubscription**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Crear una suscripción actualizable en una publicación transaccional](../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) [suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [sp_change_subscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
