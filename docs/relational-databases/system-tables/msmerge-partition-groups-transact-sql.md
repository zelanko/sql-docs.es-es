---
title: MSmerge_partition_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_partition_groups_TSQL
- MSmerge_partition_groups
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_partition_groups system table
ms.assetid: 5d56d780-ee40-4afc-9c2a-d1723d86e430
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb8c77ba54e25c574d5f751febe8bdac3ba1dfbf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911254"
---
# <a name="msmergepartitiongroups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_partition_groups** tabla almacena una fila para cada partición precalculada de una base de datos. Además de las columnas enumeradas, en esta tabla se incluye una columna para cada función utilizada en un filtro de fila con parámetros. Por ejemplo, una columna denominada **HOST_NAME_FN** se agrega a la tabla si usa un filtro el [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función. Se almacena una fila para cada conjunto único de valores de función que se han sincronizado con este publicador. Dos o más suscriptores se sincronizan exactamente con el mismo valor para todas estas funciones, compartirán la misma fila en esta tabla y, por tanto, compartirán el mismo Id. de partición. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|Columna de identidad que proporciona un número de Id. único para la partición precalculada.|  
|**publication_number**|**smallint**|El número de publicación, que se almacena en **sysmergepublications**.|  
|**maxgen_whenadded**|**bigint**|Generación más alta que se conoce en el publicador en el momento de insertar la fila en esta tabla.|  
|**using_partition_groups**|**bit**|Indica si la partición pertenece a una publicación que utiliza particiones precalculadas, y puede tener uno de estos valores:<br /><br /> **0** = publicación no utiliza particiones precalculadas.<br /><br /> **1** = la publicación utiliza particiones precalculadas<br /><br /> Para obtener más información, vea [Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).|  
|**HOST_NAME_FN**|**nvarchar(128)**|Valor que se suministra al utilizar filtros de fila con parámetros para generar particiones. Para obtener más información, consulte [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
