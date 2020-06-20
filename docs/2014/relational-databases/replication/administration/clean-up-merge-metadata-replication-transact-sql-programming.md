---
title: Limpieza de metadatos de mezcla (programación de la replicación con Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5a2306db72fd3f0098e18ff058796a5498eafcac
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043334"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>Limpiar metadatos de mezcla (programación de la replicación con Transact-SQL)
  El Agente de mezcla limpia periódicamente los metadatos de replicación de mezcla según la configuración de retención de la publicación. Esto tiene lugar en el publicador y en el suscriptor de las tablas del sistema [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql), [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql), [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)y [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) . También puede limpiar mediante programación los datos de estas tablas utilizando procedimientos almacenados de la replicación.  
  
### <a name="to-manually-clean-up-merge-metadata"></a>Para limpiar manualmente los metadatos de mezcla  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_mergemetadataretentioncleanup](/sql/relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql).  
  
2.  Opta Tenga en cuenta el número de filas que se han quitado en el paso 1 de las tablas del sistema [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql), [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)y [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql) , devueltas respectivamente en los **@num_genhistory_rows** parámetros de **@num_contents_rows** salida, y **@num_tombstone_rows** .  
  
3.  Repita los pasos 1 y 2 en el suscriptor para limpiar los metadatos en la base de datos de suscripciones.  
  
## <a name="see-also"></a>Consulte también  
 [Desactivación y expiración de las suscripciones](../subscription-expiration-and-deactivation.md)  
  
  
