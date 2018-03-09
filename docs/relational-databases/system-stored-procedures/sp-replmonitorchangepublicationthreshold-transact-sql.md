---
title: sp_replmonitorchangepublicationthreshold (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e24fd4746ee5a93489e55b6cf16edc0150c647b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spreplmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la métrica del umbral de supervisión de una publicación. Este procedimiento almacenado, que se utiliza para supervisar la replicación, se ejecuta en el distribuidor en la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher**  =] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 Es el nombre de la base de datos publicada. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication**  =] **'***publicación***'**  
 Es el nombre de la publicación para la que se cambian los atributos del umbral de supervisión. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication_type**  =] *publication_type*  
 Es el tipo de publicación. *publication_type* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Publicación transaccional.|  
|**1**|Publicación de instantáneas.|  
|**2**|Publicación de combinación.|  
|NULL (predeterminado)|La replicación intenta determinar el tipo de publicación.|  
  
 [  **@metric_id**  =] *metric_id*  
 Es el identificador de la métrica de umbral de publicación que se va a cambiar. *metric_id* es **int**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Valor|Nombre de la métrica|  
|-----------|-----------------|  
|**1**|**expiration** : supervisa la expiración inminente de suscripciones a publicaciones transaccionales.|  
|**2**|**latency** : supervisa el rendimiento de suscripciones a publicaciones transaccionales.|  
|**4**|**mergeexpiration** : supervisa la expiración inminente de suscripciones a publicaciones de combinación.|  
|**5**|**mergeslowrunduration** -supervisa la duración de sincronizaciones de mezcla en conexiones de ancho de banda bajo (telefónico).|  
|**6**|**mergefastrunduration** -supervisa la duración de sincronizaciones de mezcla en conexiones de red de área local de gran ancho de banda (LAN).|  
|**7**|**mergefastrunspeed** : supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de red de área local (LAN) de gran ancho de banda.|  
|**8**|**mergeslowrunspeed** -supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de ancho de banda bajo (telefónico).|  
  
 Debe especificar *metric_id* o *thresholdmetricname*. Si *thresholdmetricname* no se especifica, *metric_id* debe ser NULL.  
  
 [  **@thresholdmetricname**  =] **'***thresholdmetricname***'**  
 Es el nombre de la métrica de umbral de publicación que se va a cambiar. *thresholdmetricname* es **sysname**, su valor predeterminado es null. Debe especificar *thresholdmetricname* o *metric_id*. Si *metric_id* no se especifica, *thresholdmetricname* debe ser NULL.  
  
 [  **@value**  =] *valor*  
 Es el nuevo valor de la métrica de umbral de la publicación. *valor* es **int**, su valor predeterminado es null. Si **null**, a continuación, el valor de métrica no se actualiza.  
  
 [  **@shouldalert**  =] *shouldalert*  
 Especifica si se debe generar una alerta al alcanzar la métrica de umbral de una publicación. *shouldalert* es **bits**, su valor predeterminado es null. Un valor de **1** significa que se genera una alerta y el valor de **0** significa que no se generará una alerta.  
  
 [  **@mode**  =] *modo*  
 Especifica si se habilita la métrica de umbral de la publicación. *modo* es **tinyint**, su valor predeterminado es **1**. Un valor de **1** significa que la supervisión de esta métrica está habilitada y el valor de **2** significa que la supervisión de esta métrica está deshabilitada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorchangepublicationthreshold** se utiliza con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **db_owner** o **replmonitor** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_replmonitorchangepublicationthreshold**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
