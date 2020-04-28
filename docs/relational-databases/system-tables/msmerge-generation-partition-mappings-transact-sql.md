---
title: MSmerge_generation_partition_mappings (T-SQL)
description: Describe el MSmerge_generation_partition_mappings procedimiento almacenado que se utiliza para realizar el seguimiento de los cambios en las particiones en una publicación de combinación.
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_generation_partition_mappings_TSQL
- MSmerge_generation_partition_mappings
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_generation_partition_mappings system table
ms.assetid: 443a4024-ce48-4772-9ee5-95bd6fb6476b
author: stevestein
ms.author: sstein
ms.openlocfilehash: a43f4b3fac5f237904d0160ccfbde4b88f9a3616
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75322117"
---
# <a name="msmerge_generation_partition_mappings-transact-sql"></a>MSmerge_generation_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSmerge_generation_partition_mappings** se utiliza para realizar el seguimiento de los cambios en las particiones en una publicación de combinación. Esta tabla se almacena en las bases de datos de publicación y scubscription.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|Identifica la publicación de combinación.|  
|**última**|**bigint**|Valor de generación.|  
|**partition_id**|**int**|Identifica la partición.|  
|**changecount**|**int**|Número de veces que la partición ha cambiado.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
