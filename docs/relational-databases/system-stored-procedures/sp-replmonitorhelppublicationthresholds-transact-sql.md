---
title: sp_replmonitorhelppublicationthresholds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelppublicationthresholds
- sp_replmonitorhelppublicationthresholds_TSQL
helpviewer_keywords:
- sp_replmonitorhelppublicationthresholds
ms.assetid: d6b1aa4b-3369-4255-a892-c0e5cc9cb693
author: stevestein
ms.author: sstein
ms.openlocfilehash: ac1efa2e63bb798ce24785e4240bd756e8737e51
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771203"
---
# <a name="spreplmonitorhelppublicationthresholds-transact-sql"></a>sp_replmonitorhelppublicationthresholds (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos publicada. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publication_type = ] publication_type`Si el tipo de publicación. *publication_type* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Publicación transaccional.|  
|**1**|Publicación de instantáneas.|  
|**2**|Publicación de combinación.|  
|NULL (predeterminado)|La replicación intenta determinar el tipo de publicación.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Id. de la métrica del rendimiento de la replicación, que puede tener uno de los siguientes valores.<br /><br /> **1expiration** : supervisa la expiración inminente de las suscripciones a las publicaciones transaccionales.<br /><br /> **2latency** : supervisa el rendimiento de las suscripciones a las publicaciones transaccionales.<br /><br /> **4mergeexpiration** : supervisa la expiración inminente de suscripciones a publicaciones de combinación.<br /><br /> **5mergeslowrunduration** : supervisa la duración de las sincronizaciones de mezcla en conexiones de bajo ancho de banda (acceso telefónico).<br /><br /> **6mergefastrunduration** : supervisa la duración de las sincronizaciones de mezcla en conexiones de gran ancho de banda (LAN).<br /><br /> **7mergefastrunspeed** : supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de gran ancho de banda (LAN).<br /><br /> **8mergeslowrunspeed** : supervisa la velocidad de sincronización de sincronizaciones de mezcla en conexiones de bajo ancho de banda (acceso telefónico).|  
|**title**|**sysname**|Nombre de la métrica de rendimiento de la replicación.|  
|**value**|**int**|El valor de umbral de la métrica de rendimiento.|  
|**shouldalert**|**bit**|Indica si se debe generar una alerta cuando la métrica supera el umbral definido para esta publicación. un valor de **1** indica que debe generarse una alerta.|  
|**isenabled**|**bit**|Es si la supervisión está habilitada para esta métrica de rendimiento de replicación para esta publicación. un valor de **1** indica que está habilitada la supervisión.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorhelppublicationthresholds** se usa con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de base de datos **db_owner** o **replmonitor** de la base de datos de distribución pueden ejecutar **sp_replmonitorhelppublicationthresholds**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
