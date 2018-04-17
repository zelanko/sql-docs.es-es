---
title: sp_replmonitorhelppublication (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_replmonitorhelppublication_TSQL
- sp_replmonitorhelppublication
helpviewer_keywords:
- sp_replmonitorhelppublication
ms.assetid: 7928c50c-617f-41c5-9e0f-4e42e8be55dc
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 880ceb504a2ad8fba418374db362fa0574dfa9c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spreplmonitorhelppublication-transact-sql"></a>sp_replmonitorhelppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve la información de estado actual para una o varias publicaciones del publicador. Este procedimiento almacenado, que se utiliza para supervisar la replicación, se ejecuta en el distribuidor en la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorhelppublication [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publisher_db'   
    [ , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador cuyo estado se está supervisando. *Publisher* es **sysname**, su valor predeterminado es null. Si **null**, se devolverá información para todos los publicadores que utilizan el distribuidor.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 Es el nombre de la base de datos publicada. *publisher_db* es **sysname**, su valor predeterminado es null. Si es NULL, se devuelve información sobre todas las bases de datos publicadas en el publicador.  
  
 [ **@publication** =] **'***publicación***'**  
 Es el nombre de la publicación que se está supervisando. *publicación* es **sysname**, su valor predeterminado es null.  
  
 [ **@publication_type** =] *publication_type*  
 Es el tipo de publicación. *publication_type* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Publicación transaccional.|  
|**1**|Publicación de instantáneas.|  
|**2**|Publicación de combinación.|  
|NULL (predeterminado)|La replicación intenta determinar el tipo de publicación.|  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Exclusivamente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publisher_db**|**sysname**|Es el nombre del publicador.|  
|**Publicación**|**sysname**|Es el nombre de una publicación.|  
|**publication_type**|**int**|Es el tipo de publicación y puede tener uno de los valores siguientes.<br /><br /> **0** = publicación transaccional<br /><br /> **1** = publicación de instantáneas<br /><br /> **2** = publicación de combinación|  
|**status**|**int**|Estado máximo de todos los agentes de replicación asociados a la publicación. Puede ser uno de estos valores.<br /><br /> **1** = iniciado<br /><br /> **2** = se ha realizado correctamente<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintentando<br /><br /> **6** = error|  
|**Advertencia**|**int**|Advertencia de umbral máximo generada por una suscripción que pertenece a la publicación, que puede ser el resultado de OR lógico de uno o más de estos valores.<br /><br /> **1** = expiration: una suscripción a una publicación transaccional no se ha sincronizado dentro del umbral de período de retención.<br /><br /> **2** = latency: el tiempo que tarda en replicar datos desde un publicador transaccional al suscriptor supera el umbral, en segundos.<br /><br /> **4** = mergeexpiration: una suscripción a una publicación de combinación no se ha sincronizado dentro del umbral de período de retención.<br /><br /> **8** = mergefastrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red rápida.<br /><br /> **16** = mergeslowrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red lenta o telefónico.<br /><br /> **32** = mergefastrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, en una conexión de red rápida.<br /><br /> **64** = mergeslowrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, en una conexión de red lenta o telefónico.|  
|**worst_latency**|**int**|La mayor latencia, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG para una publicación transaccional.|  
|**best_latency**|**int**|La menor latencia, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG para una publicación transaccional.|  
|**average_latency**|**int**|La latencia promedio, en segundos, para los cambios de datos propagados por los agentes de distribución o de registro del LOG para una publicación transaccional.|  
|**last_distsync**|**datetime**|Es el valor de datetime correspondiente a la última ejecución del Agente de distribución.|  
|**Retención**|**int**|Es el período de retención de la publicación.|  
|**LatencyThreshold**|**int**|Es el umbral de latencia definido para la publicación transaccional.|  
|**expirationthreshold**|**int**|Es el umbral de expiración definido para la publicación si se trata de una publicación de combinación.|  
|**agentnotrunningthreshold**|**int**|Es el umbral definido para el período de tiempo más largo transcurrido sin que se haya ejecutado un agente.|  
|**subscriptioncount**|**int**|Es el número de suscripciones de una publicación.|  
|**runningdistagentcount**|**int**|Es el número de agentes de distribución que se están ejecutando para la publicación.|  
|**snapshot_agentname**|**sysname**|Nombre del trabajo del Agente de instantáneas para la publicación.|  
|**logreader_agentname**|**sysname**|Nombre del trabajo del Agente de registro del LOG para la publicación transaccional.|  
|**qreader_agentname**|**sysname**|Nombre del trabajo del Agente de lectura de cola para una publicación transaccional que admite la actualización en cola.|  
|**worst_runspeedPerf**|**int**|Es el mayor tiempo de sincronización de la publicación de combinación.|  
|**best_runspeedPerf**|**int**|Es el menor tiempo de sincronización de la publicación de combinación.|  
|**average_runspeedPerf**|**int**|Es el tiempo medio de sincronización de la publicación de combinación.|  
|**retention_period_unit**|**int**|Es la unidad que se utiliza para expresar *retención*.|  
|**publicador**|**sysname**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publica la publicación.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorhelppublication** se utiliza con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **db_owner** o **replmonitor** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_replmonitorhelppublication**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
