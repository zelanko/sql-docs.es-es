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
ms.openlocfilehash: 362735d33f835c7b66e4f0994fd5c4ff6f084f15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68102192"
---
# <a name="msmerge_partition_groups-transact-sql"></a>MSmerge_partition_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En la tabla **MSmerge_partition_groups** se almacena una fila por cada partición precalculada en una base de datos determinada. Además de las columnas enumeradas, en esta tabla se incluye una columna para cada función utilizada en un filtro de fila con parámetros. Por ejemplo, se agrega una columna denominada **HOST_NAME_FN** a la tabla si un filtro utiliza la función [host_name](../../t-sql/functions/host-name-transact-sql.md) . Se almacena una fila para cada conjunto único de valores de función que se han sincronizado con este publicador. Si dos o más suscriptores se sincronizan exactamente con el mismo valor para todas estas funciones, compartirán la misma fila de esta tabla y, por tanto, compartirán el mismo Id. de partición. Esta tabla se almacena en la base de datos de publicaciones.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|Columna de identidad que proporciona un número de Id. único para la partición precalculada.|  
|**publication_number**|**smallint**|El número de publicación, que se almacena en **sysmergepublications**.|  
|**maxgen_whenadded**|**BIGINT**|Generación más alta que se conoce en el publicador en el momento de insertar la fila en esta tabla.|  
|**using_partition_groups**|**bit**|Indica si la partición pertenece a una publicación que utiliza particiones precalculadas, y puede tener uno de estos valores:<br /><br /> **0** = la publicación no utiliza particiones precalculadas.<br /><br /> **1** = la publicación utiliza particiones precalculadas<br /><br /> Para obtener más información, vea [Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).|  
|**HOST_NAME_FN**|**nvarchar(128)**|Valor que se suministra al utilizar filtros de fila con parámetros para generar particiones. Para obtener más información, consulte [Filtros de fila con parámetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
