---
title: MSmerge_genhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
author: stevestein
ms.author: sstein
ms.openlocfilehash: bf9c38fe71c1282b19b947fc1771714dd138c45a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017703"
---
# <a name="msmergegenhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_genhistory** tabla contiene una fila por cada generación que constancia un suscriptor (dentro del período de retención). Se utiliza para evitar enviar las generaciones comunes durante los intercambios y para volver a sincronizar los suscriptores restaurados a partir de copias de seguridad. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|Identificador global de los cambios que ha identificado la generación en el suscriptor.|  
|**pubid**|**uniqueidentifier**|Identificador de publicación.|  
|**generation**|**bigint**|Valor de generación.|  
|**art_nick**|**int**|El alias del artículo.|  
|**Alias**|**varbinary(1001)**|Lista de alias de otros suscriptores de los que se conoce que han tenido esta generación. Se usa para evitar enviar una generación a un suscriptor que ya ha visto los cambios. Los alias de la lista se mantienen ordenados para que las búsquedas sean más eficaces. Si hay más alias de los que caben en el campo, no podrán aprovechar esta optimización.|  
|**colDate**|**datetime**|Fecha en que se agrega la generación actual a la tabla.|  
|**genstatus**|**tinyint**|La generación puede tener los estados siguientes:<br /><br /> **0** = abierta.<br /><br /> **1** = cerrada.<br /><br /> **2** = cerrada y originada en otro suscriptor.|  
|**changecount**|**int**|Número de cambios reflejados en una generación dada.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
