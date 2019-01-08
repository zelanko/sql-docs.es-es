---
title: MSreplication_queue (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c2370bfc06f9fd939f5778ad52e6cb09aeae2806
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819073"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplication_queue** tabla se utiliza el proceso de replicación para almacenar los comandos en cola emitidos por todas las suscripciones de actualización en cola que utilizan basado en SQL en la cola. Esta tabla se almacena en la base de datos de suscripción.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|El nombre del publicador.|  
|**publisher_db**|**sysname**|El nombre de la base de datos de publicación.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**transacción**|**sysname**|Id. de transacción bajo el que se ha ejecutado el comando en cola.|  
|**data**|**varbinary(8000)**|Secuencia de bytes empaquetados que almacena información acerca del comando en cola.|  
|**datalen**|**int**|Longitud de los datos, en bytes.|  
|**CommandType**|**int**|Tipo de comando en la cola:<br /><br /> 1 = Comando de usuario en la transacción.<br /><br /> 2 = Comando de sincronización de suscripción.|  
|**insertdate**|**datetime**|Fecha de inserción.|  
|**orderkey**|**bigint**|Columna de identidad con una progresión continua.|  
|**cmdstate**|**bit**|Estado del comando:<br /><br /> 0 = Completo.<br /><br /> 1 = Parcial.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
