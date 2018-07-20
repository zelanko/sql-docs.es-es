---
title: MSmerge_tombstone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af64c598ccb092a5c0e408496ceba8d97f609124
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102073"
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
  
  
