---
title: MSreplication_queue (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
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
- MSreplication_queue
- MSreplication_queue_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_queue system table
ms.assetid: 664bf817-8021-4417-96d6-2bb1e4baabff
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1230ab84f1d5082fd1f8b9482702a9361b7b9f2e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33005512"
---
# <a name="msreplicationqueue-transact-sql"></a>MSreplication_queue (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSreplication_queue** tabla participa en el proceso de replicación para almacenar los comandos en cola emitidos por todas las suscripciones de actualización en cola que utilizan basado en SQL en la cola. Esta tabla se almacena en la base de datos de suscripción.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|El nombre del publicador.|  
|**publisher_db**|**sysname**|El nombre de la base de datos de publicación.|  
|**Publicación**|**sysname**|Nombre de la publicación.|  
|**Transacción**|**sysname**|Id. de transacción bajo el que se ha ejecutado el comando en cola.|  
|**data**|**varbinary(8000)**|Secuencia de bytes empaquetados que almacena información acerca del comando en cola.|  
|**datalen**|**int**|Longitud de los datos, en bytes.|  
|**CommandType**|**int**|Tipo de comando en la cola:<br /><br /> 1 = Comando de usuario en la transacción.<br /><br /> 2 = Comando de sincronización de suscripción.|  
|**insertdate**|**datetime**|Fecha de inserción.|  
|**orderkey**|**bigint**|Columna de identidad con una progresión continua.|  
|**cmdstate**|**bit**|Estado del comando:<br /><br /> 0 = Completo.<br /><br /> 1 = Parcial.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
