---
title: MSmerge_identity_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSmerge_identity_range_TSQL
- MSmerge_identity_range
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_identity_range system table
ms.assetid: 493a2028-88a0-4e83-ad89-ae5661d9f477
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 623914f556064f690c0883e41316c76e84c3c7e3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854773"
---
# <a name="msmergeidentityrange-transact-sql"></a>MSmerge_identity_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_identity_range** tabla se utiliza para realizar un seguimiento de los intervalos numéricos asignados a las columnas de identidad para la suscripción a publicaciones en el que la replicación se administran automáticamente estas asignaciones de intervalos. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**subid**|**uniqueidentifier**|Número de identificación único para una suscripción dada.|  
|**artid**|**uniqueidentifier**|El número de identificación único del artículo indicado.|  
|**range_begin**|**numeric(38)**|Valor de identidad al principio del intervalo actual.|  
|**range_end**|**numeric(38)**|Valor de identidad al final del intervalo actual.|  
|**next_range_begin**|**numeric(38)**|Valor de identidad al principio del siguiente intervalo que se va a asignar.|  
|**next_range_end**|**numeric(38)**|Valor de identidad al final del siguiente intervalo que se va a asignar.|  
|**is_pub_range**|**bit**|Un valor de **1** si el intervalo de identidad se asigna a la publicación.|  
|**max_used**|**numeric(38)**|Valor de identidad máximo que se puede asignar.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
