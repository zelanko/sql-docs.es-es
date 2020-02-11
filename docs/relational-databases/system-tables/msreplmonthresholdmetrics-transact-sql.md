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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079942"
---
# <a name="msreplmonthresholdmetrics-transact-sql"></a>MSreplmonthresholdmetrics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSreplmonthresholdmetrics** define las métricas proporcionadas para la supervisión de la replicación. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**metric_id**|**int**|Identifica una métrica de rendimiento de replicación y puede ser uno de los siguientes valores:<br /><br /> **1** = expiración<br /><br /> **2** = latencia<br /><br /> **4** = mergeexpiration<br /><br /> **5** = mergeslowrunduration<br /><br /> **6** = mergefastrunduration<br /><br /> **7** = mergefastrunspeed<br /><br /> **8** = mergeslowrunspeed|  
|**Titulo**|**sysname**|Nombre de la medición de rendimiento de replicación.|  
|**warningbitstatus**|**int**|Identificador bit a bit utilizado para proporcionar una advertencia de infracción de umbral de una de las siguientes mediciones:<br /><br /> **1** = expiración: una suscripción a una publicación transaccional ha superado el período de retención por encima del umbral permitido, como un porcentaje del período de retención.<br /><br /> **2** = latencia: el tiempo que se tarda en replicar los datos de un publicador transaccional en el suscriptor supera el umbral, en segundos.<br /><br /> **4** = Mergeexpiration: una suscripción a una publicación de combinación ha superado el período de retención por encima del umbral permitido, como un porcentaje del período de retención.<br /><br /> **8** = Mergefastrunduration: el tiempo que se tarda en completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red rápida.<br /><br /> **16** = Mergeslowrunduration: el tiempo que se tarda en completar la sincronización de una suscripción de mezcla supera el umbral, en segundos, a través de una conexión de red lenta o de acceso telefónico.<br /><br /> **32** = Mergefastrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, en una conexión de red rápida.<br /><br /> **64** = Mergeslowrunspeed: la tasa de entrega de filas durante la sincronización de una suscripción de mezcla no ha podido mantener la tasa de umbral, en filas por segundo, en una conexión de red lenta o de acceso telefónico.|  
|**alertmessageid**|**int**|Id. del mensaje de error que se muestra cuando se produce la condición de advertencia de umbral.|  
|**denominación**|**nvarchar (3000)**|Descripción de la medición de rendimiento de replicación.|  
|**default_value**|**sql_variant**|Valor predeterminado para la medición de rendimiento de replicación.|  
|**min_value**|**sql_variant**|Valor mínimo de una medición de rendimiento de replicación enlazada.|  
|**max_value**|**sql_variant**|Valor máximo de una medición de rendimiento de replicación enlazada.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
