---
title: sp_helpmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad32cd5b8e6936bc646fa664052a307a9e0d7ed0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779377"
---
# <a name="sphelpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre una suscripción a una publicación de combinación, tanto de inserción como de extracción. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones o en el suscriptor de republicaciones de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**. La publicación debe existir y debe cumplir las normas de los identificadores. Si es NULL o **%**, se devuelve información sobre todas las publicaciones de combinación y suscripciones en la base de datos actual.  
  
 [  **@subscriber=**] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es **%**. Si es NULL o %, se devuelve información acerca de todas las suscripciones a la publicación dada.  
  
 [  **@subscriber_db=**] **'***subscriber_db***'**  
 Es el nombre de la base de datos de suscripción. *subscriber_db*es **sysname**, su valor predeterminado es **%**, que devuelve información sobre todas las bases de datos de suscripción.  
  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. El publicador debe ser un servidor válido. *publicador*es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todos los publicadores.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Es el nombre de la base de datos del publicador. *publisher_db*es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todas las bases de datos del publicador.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 Es el tipo de suscripción. *subscription_type*es **nvarchar (15)**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**inserción** (valor predeterminado)|Suscripción de inserción.|  
|**Incorporación de cambios**|Suscripción de extracción|  
|**ambos**|Suscripción de inserción y extracción|  
  
 [  **@found=**] **'***encuentra***' salida**  
 Es una marca para indicar que se devuelven filas. *se encontró*es **int** y un parámetro OUTPUT y su valor predeterminado es null. **1** indica que se encuentra la publicación. **0** indica que no se encuentra la publicación.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|Nombre de la suscripción.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**publicador**|**sysname**|Nombre del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**suscriptor**|**sysname**|Nombre del suscriptor.|  
|**subscriber_db**|**sysname**|Nombre de la base de datos de suscripciones.|  
|**status**|**int**|Estado de la suscripción:<br /><br /> **0** todos los = trabajos están esperando para iniciar<br /><br /> **1** = uno o más trabajos se están iniciando<br /><br /> **2** = todos los trabajos se han ejecutado correctamente<br /><br /> **3** = al menos un trabajo se está ejecutando<br /><br /> **4** = todos los trabajos están programados y se encuentran inactivos<br /><br /> **5** = al menos un trabajo intenta ejecutarse después de un error anterior<br /><br /> **6** = al menos un trabajo no ha podido ejecutar correctamente|  
|**propiedad subscriber_type**|**int**|Tipo de suscriptor.|  
|**subscription_type**|**int**|Tipo de suscripción:<br /><br /> **0** = inserción<br /><br /> **1** = extracción<br /><br /> **2** = both|  
|**priority**|**float(8)**|Número que indica la prioridad de la suscripción.|  
|**sync_type**|**tinyint**|Tipo de sincronización de la suscripción.|  
|**description**|**nvarchar(255)**|Breve descripción de esta suscripción de mezcla.|  
|**merge_jobid**|**binary (16)**|Id. de trabajo del Agente de mezcla.|  
|**full_publication**|**tinyint**|Indica si la suscripción es a una publicación completa o filtrada.|  
|**offload_enabled**|**bit**|Especifica si se ha establecido que la ejecución de la descarga de un agente de replicación se lleve a cabo en el suscriptor. Si es NULL, la ejecución se lleva a cabo en el publicador.|  
|**offload_server**|**sysname**|Nombre del servidor donde se está ejecutando el agente.|  
|**use_interactive_resolver**|**int**|Devuelve si se utiliza o no el solucionador interactivo durante la reconciliación. Si **0**, no se utiliza el solucionador interactivo.|  
|**Nombre de host**|**sysname**|Valor suministrado cuando una suscripción se filtra por el valor de la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función.|  
|**subscriber_security_mode**|**smallint**|Es el modo de seguridad en el suscriptor, donde **1** significa autenticación de Windows y **0** significa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**subscriber_login**|**sysname**|Es el nombre de inicio de sesión del suscriptor.|  
|**subscriber_password**|**sysname**|La contraseña real del suscriptor no se devuelve nunca. El resultado se enmascara mediante una "**\*\*\*\*\*\***" cadena.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergesubscription** se utiliza en la replicación de mezcla para devolver información de suscripción almacenada en el publicador o suscriptor de republicación.  
  
 Las suscripciones anónimas, el *subscription_type*valor siempre es **1** (extracción). Sin embargo, debe ejecutar [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) en el suscriptor para obtener información sobre suscripciones anónimas.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos o la lista de acceso de publicación para la publicación a la que pertenece la suscripción puede ejecutar **sp_ helpmergesubscription**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
