---
title: MSmerge_tombstone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab57e69118edfe4a647d6baeedf5a10ee8460247
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796265"
---
# <a name="msmergetombstone-transact-sql"></a>MSmerge_tombstone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_tombstone** tabla contiene información sobre las filas eliminadas y permite las eliminaciones se propagan a otros suscriptores. Esta tabla se almacena en las bases de datos de publicación y de suscripciones.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|Identificador de fila.|  
|**tablenick**|**int**|Alias de la tabla.|  
|**Tipo**|**tinyint**|Tipo de eliminación:<br /><br /> 1 = Eliminación de usuario.<br /><br /> 5 = La fila ya no pertenece a la partición filtrada.<br /><br /> 6 = Eliminación de sistema.|  
|**linaje**|**varbinary(249)**|Indica la versión del registro eliminada y las actualizaciones conocidas antes de su eliminación. Permite usar reglas para la resolución coherente de un conflicto cuando un suscriptor actualiza una fila mientras otro suscriptor la elimina.|  
|**generación**|**int**|Se asigna cuando se elimina una fila. Si un suscriptor solicita la generación N, solamente se envían marcadores de exclusión con generación >= N.|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|Identifica el registro lógico al que pertenece una fila eliminada.|  
|**logical_record_lineage**|**Varbinary(501)**|El alias del suscriptor, pares de números de versión que se utilizan para mantener un historial de las eliminaciones del registro lógico al que pertenece esta fila.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
