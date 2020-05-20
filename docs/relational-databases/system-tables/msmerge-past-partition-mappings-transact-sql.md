---
title: MSmerge_past_partition_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_past_partition_mappings
- MSmerge_past_partition_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_past_partition_mappings system table
ms.assetid: 06d54ff5-4d29-4eeb-b8be-64d032e53134
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9faca4ae8492f7ec0c784b05b16799c5b5b398ae
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827239"
---
# <a name="msmerge_past_partition_mappings-transact-sql"></a>MSmerge_past_partition_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En la tabla **MSmerge_past_partition_mappings** se almacena una fila por cada ID. de partición al que se usa una fila modificada determinada a la que pertenece, pero que ya no pertenece a. Esta tabla se almacena en la base de datos de publicación.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publication_number**|**smallint**|El número de publicación, que se almacena en **sysmergepublications**.|  
|**tablenick**|**int**|El alias de la tabla publicada.|  
|**rowguid**|**uniqueidentifier**|Identificador de la fila especificada.|  
|**partition_id**|**int**|Id. de la partición a la que pertenece la fila. El valor es-1 si el cambio de la fila es relevante para todos los suscriptores.|  
|**última**|**bigint**|Valor de la generación en la que se ha producido el cambio de partición.|  
|**reason**|**tinyint**|Solo para uso interno.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
