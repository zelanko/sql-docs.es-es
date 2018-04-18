---
title: sp_replmonitorhelppublisher (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
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
- sp_replmonitorhelppublisher_TSQL
- sp_replmonitorhelppublisher
helpviewer_keywords:
- sp_replmonitorhelppublisher
ms.assetid: 171501fe-4b74-4647-96c3-7691c777e01b
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca7ba5f15c56eef17808510dbf1a33de5f6fadc3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spreplmonitorhelppublisher-transact-sql"></a>sp_replmonitorhelppublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre el estado actual para uno o más publicadores asociados a un distribuidor. Este procedimiento almacenado, que se utiliza para supervisar la replicación, se ejecuta en el distribuidor en la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorhelppublisher [ [ @publisher = ] 'publisher' ]  
    [ , [ @refreshpolicy = ] refreshpolicy ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador cuyo estado se está supervisando. *Publisher* es **sysname**, su valor predeterminado es null. Si el valor es NULL, se devuelve información para todos los publicadores que utilizan el distribuidor.  
  
 [  **@refreshpolicy=** ] *refreshpolicy*  
 Exclusivamente para uso interno.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|Es el nombre de un publicador.|  
|**distribution_db**|**sysname**|Es el nombre de la base de datos de distribución utilizada por un publicador.|  
|**status**|**int**|Estado máximo de todos los agentes de replicación asociados a las publicaciones de este publicador, el cual puede ser uno de los valores siguientes.<br /><br /> **1** = iniciado<br /><br /> **2** = se ha realizado correctamente<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintentando<br /><br /> **6** = error|  
|**Advertencia**|**int**|Advertencia de umbral máximo generada por una suscripción perteneciente a una publicación de este publicador, la cual puede ser el resultado lógico OR de uno o más de estos valores.<br /><br /> **1** = expiration: una suscripción a una publicación transaccional no se ha sincronizado dentro del umbral de período de retención.<br /><br /> **2** = latency: el tiempo que tarda en replicar datos desde un publicador transaccional al suscriptor supera el umbral, en segundos.<br /><br /> **4** = mergeexpiration: una suscripción a una publicación de combinación no se ha sincronizado dentro del umbral de período de retención.<br /><br /> **8** = mergefastrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red rápida.<br /><br /> **16** = mergeslowrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red lenta o telefónico.<br /><br /> **32** = mergefastrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, en una conexión de red rápida.<br /><br /> **64** = mergeslowrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, en una conexión de red lenta o telefónico.|  
|**publicationcount**|**int**|Es el número de publicaciones pertenecientes al publicador.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorhelppublisher** se utiliza con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor o los miembros de la **db_owner** o **replmonitor** pueden roles fijos de base de datos en la base de datos de distribución ejecutar **sp_replmonitorhelppublisher**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
