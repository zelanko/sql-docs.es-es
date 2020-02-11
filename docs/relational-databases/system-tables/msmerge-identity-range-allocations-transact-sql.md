---
title: MSmerge_identity_range_allocations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_allocations
- MSmerge_identity_range_allocations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range_allocations system table
ms.assetid: 6362e35e-0ab3-4638-855b-1ce013f5fd6d
author: stevestein
ms.author: sstein
ms.openlocfilehash: de0325925bb1ad1626987361435056ff21a26be6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68072655"
---
# <a name="msmerge_identity_range_allocations-transact-sql"></a>MSmerge_identity_range_allocations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla **MSmerge_identity_range_allocations** se usa para realizar un seguimiento del historial de las asignaciones de intervalos de identidad, tanto para los publicadores como para los suscriptores, para los artículos publicados. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|IDENTIFICADOR del publicador.|  
|**publisher_db**|**nvarchar(128)**|Nombre de la base de datos de publicación.|  
|**publicaciones**|**nvarchar(128)**|Nombre de la publicación.|  
|**ARTICLE**|**nvarchar(128)**|Nombre del artículo.|  
|**suscriptor**|**nvarchar(128)**|Nombre del suscriptor.|  
|**subscriber_db**|**nvarchar(128)**|El nombre de la base de datos de suscripciones.|  
|**is_pub_range**|**bit**|Muestra si el intervalo de identidad está asignado a un publicador.|  
|**ranges_allocated**|**tinyint**|Número de intervalos de identidad asignados.|  
|**range_begin**|**Numeric (38)**|Valor inicial del intervalo.|  
|**range_end**|**Numeric (38)**|Último valor del intervalo.|  
|**next_range_begin**|**Numeric (38)**|Valor inicial del siguiente intervalo que se va a asignar.|  
|**next_range_end**|**Numeric (38)**|Último valor del siguiente intervalo que se va a asignar.|  
|**max_used**|**Numeric (38)**|Mayor valor de identidad utilizado.|  
|**time_of_allocation**|**datetime**|Hora en la que se realizó la asignación.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
