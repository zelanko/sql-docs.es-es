---
title: MSreplmonthresholdmetrics (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- msreplmonthresholdmetrics_TSQL
- msreplmonthresholdmetrics
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplmonthresholdmetrics system table
ms.assetid: 0cc9b40a-36ce-485b-9bc2-d4abd5aa6727
author: stevestein
ms.author: sstein
ms.openlocfilehash: b3e8b9c2443a6fa74e113dc1a3f25880ac753dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079942"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplmonthresholdmetrics** tabla define las métricas proporcionadas para supervisar la replicación. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Identifica una métrica de rendimiento de replicación y puede ser uno de los siguientes valores:<br /><br /> **1** = expiración<br /><br /> **2** = latency<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**title**|**sysname**|Nombre de la medición de rendimiento de replicación.|  
|**warningbitstatus**|**int**|Identificador bit a bit utilizado para proporcionar una advertencia de infracción de umbral de una de las siguientes mediciones:<br /><br /> **1** = expiration: una suscripción a una publicación transaccional ha superado el período de retención por encima del umbral permitido, como un porcentaje del período de retención.<br /><br /> **2** = latency: el tiempo necesario para replicar datos desde un publicador transaccional al suscriptor supera el umbral, en segundos.<br /><br /> **4** = mergeexpiration: una suscripción a una publicación de combinación ha superado el período de retención por encima del umbral permitido, como un porcentaje del período de retención.<br /><br /> **8** = mergefastrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red rápida.<br /><br /> **16** = mergeslowrunduration: el tiempo necesario para completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red lenta o telefónico.<br /><br /> **32** = mergefastrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, a través de una conexión de red rápida.<br /><br /> **64** = mergeslowrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, a través de una conexión de red lenta o telefónico.|  
|**alertmessageid**|**int**|Id. del mensaje de error que se muestra cuando se produce la condición de advertencia de umbral.|  
|**description**|**nvarchar(3000)**|Descripción de la medición de rendimiento de replicación.|  
|**default_value**|**sql_variant**|Valor predeterminado para la medición de rendimiento de replicación.|  
|**MIN_VALUE**|**sql_variant**|Valor mínimo de una medición de rendimiento de replicación enlazada.|  
|**max_value**|**sql_variant**|Valor máximo de una medición de rendimiento de replicación enlazada.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
