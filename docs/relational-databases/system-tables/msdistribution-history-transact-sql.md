---
title: MSdistribution_history (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdistribution_history
- MSdistribution_history_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistribution_history system table
ms.assetid: 55665bd2-9e1d-4efc-8f60-c63a24f66b28
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 319d80ea027cd4f639c939aee0bba97745edc428
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="msdistributionhistory-transact-sql"></a>MSdistribution_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdistribution_history** tabla contiene filas de historial para los agentes de distribución asociados al distribuidor local. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|Id. del Agente de distribución.|  
|**runstatus**|**int**|El estado de ejecución:<br /><br /> **1** = inicio.<br /><br /> **2** = sea correcta.<br /><br /> **3** = en curso.<br /><br /> **4** = inactivo.<br /><br /> **5** = reintento.<br /><br /> **6** = error.|  
|**start_time**|**datetime**|Hora a la que comienza la ejecución del trabajo.|  
|**time**|**datetime**|Hora a la que se registra el mensaje.|  
|**duration**|**int**|Duración, en segundos, de la sesión del mensaje.|  
|**Comentarios**|**nvarchar(4000)**|El texto del mensaje.|  
|**xact_seqno**|**varbinary (16)**|Número de secuencia de la última transacción procesada.|  
|**current_delivery_rate**|**float**|Número promedio de comandos entregados por segundo desde la última entrada del historial.|  
|**current_delivery_latency**|**int**|Latencia entre la entrada del comando en la base de datos de distribución y su aplicación al suscriptor desde la última entrada del historial. En milisegundos.|  
|**delivered_transactions**|**int**|Número total de transacciones entregadas en la sesión.|  
|**delivered_commands**|**int**|El número total de comandos entregados en la sesión.|  
|**average_commands**|**int**|Número promedio de comandos entregados en la sesión.|  
|**delivery_rate**|**float**|Promedio de comandos entregados por segundo.|  
|**delivery_latency**|**int**|Latencia entre la entrada del comando en la base de datos de distribución y su aplicación al suscriptor. En milisegundos.|  
|**total_delivered_commands**|**bigint**|Número total de comandos entregados desde la creación de la suscripción.|  
|**error_id**|**int**|El identificador del error en la **MSrepl_error** tabla del sistema.|  
|**updateable_row**|**bit**|Establecido en **1** si la fila de historial se puede sobrescribir.|  
|**timestamp**|**timestamp**|La columna de marca de tiempo de esta tabla.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
