---
title: sp_replmonitorhelppublicationthresholds (Transact-SQL) | Documentos de Microsoft
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
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6fd9a16067e4a7a1f670d0d50e1b44ea949208e3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el conjunto de métricas de umbral para una publicación supervisada. Este procedimiento almacenado, que se utiliza para supervisar la replicación, se ejecuta en el distribuidor en la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorhelppublicationthresholds [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher**=] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db**=] **'***publisher_db***'**  
 Es el nombre de la base de datos publicada. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publication**=] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publication_type**=] *publication_type*  
 Es el tipo de publicación. *publication_type* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Publicación transaccional.|  
|**1**|Publicación de instantáneas.|  
|**2**|Publicación de combinación.|  
|NULL (predeterminado)|La replicación intenta determinar el tipo de publicación.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Id. de la métrica del rendimiento de la replicación, que puede tener uno de los siguientes valores.<br /><br /> **1expiration** -supervisa la expiración inminente de suscripciones a publicaciones transaccionales.<br /><br /> **2latency** -supervisa el rendimiento de las suscripciones a publicaciones transaccionales.<br /><br /> **4mergeexpiration** -supervisa la expiración inminente de suscripciones a publicaciones de mezcla.<br /><br /> **5mergeslowrunduration** -supervisa la duración de sincronizaciones de mezcla en conexiones de ancho de banda bajo (telefónico).<br /><br /> **6mergefastrunduration** -supervisa la duración de sincronizaciones de mezcla en conexiones de ancho de banda alto (LAN).<br /><br /> **7mergefastrunspeed** -supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de ancho de banda alto (LAN).<br /><br /> **8mergeslowrunspeed** -supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de ancho de banda bajo (telefónico).|  
|**title**|**sysname**|Nombre de la métrica de rendimiento de la replicación.|  
|**value**|**int**|El valor de umbral de la métrica de rendimiento.|  
|**shouldalert**|**bit**|Especifica si se debe generar una alerta cuando la métrica supera el umbral definido para esta publicación; un valor de **1** indica que debe generarse una alerta.|  
|**IsEnabled**|**bit**|Especifica si se habilita la supervisión para esta métrica de rendimiento de replicación para esta publicación; un valor de **1** indica que la supervisión está habilitada.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorhelppublicationthresholds** se utiliza con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **db_owner** o **replmonitor** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_replmonitorhelppublicationthresholds**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
