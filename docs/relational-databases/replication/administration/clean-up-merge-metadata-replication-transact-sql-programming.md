---
title: Limpieza de metadatos de mezcla (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bc7dc7491c594e55d4f27ca3003b5dcc3af90cd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Limpiar metadatos de mezcla (programación de la replicación con Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El Agente de mezcla limpia periódicamente los metadatos de replicación de mezcla según la configuración de retención de la publicación. Esto tiene lugar en el publicador y en el suscriptor de las tablas del sistema [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md), [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md), [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)y [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) . También puede limpiar mediante programación los datos de estas tablas utilizando procedimientos almacenados de la replicación.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Para limpiar manualmente los metadatos de mezcla  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md).  
  
2.  (Opcional) Tenga en cuenta el número de filas quitado en el paso 1 de las tablas del sistema [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md), [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)y [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) , devueltas  respectivamente en los parámetros de salida **@num_genhistory_rows**, **@num_contents_rows**y **@num_tombstone_rows** .  
  
3.  Repita los pasos 1 y 2 en el suscriptor para limpiar los metadatos en la base de datos de suscripciones.  
  
## <a name="see-also"></a>Ver también  
 [Desactivación y expiración de las suscripciones](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
