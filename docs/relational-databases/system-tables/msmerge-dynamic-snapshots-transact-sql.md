---
description: MSmerge_dynamic_snapshots (Transact-SQL)
title: MSmerge_dynamic_snapshots (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_dynamic_snapshots_TSQL
- MSmerge_dynamic_snapshots
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_dynamic_snapshots system table
ms.assetid: a5592b3c-731b-4fc9-ae4b-2602ed78248e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b03489bc2901bc13de483cf90e62fbc9645fab66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473237"
---
# <a name="msmerge_dynamic_snapshots-transact-sql"></a>MSmerge_dynamic_snapshots (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  En la tabla **MSmerge_dynamic_snapshots** se realiza un seguimiento de la ubicación de la instantánea de datos filtrados para cada partición definida para una publicación de combinación con filtros de fila con parámetros. Esta tabla se almacena en la base de datos de **publicación** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**partition_id**|**int**|El Id. de la partición de mezcla.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|La ubicación de la instantánea de datos filtrados de la partición.|  
|**last_updated**|**datetime**|La fecha en que se ha actualizado la instantánea de datos filtrados.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
