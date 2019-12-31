---
title: Sys. dm_exec_compute_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_compute_pools
- dm_exec_compute_pools_TSQL
- dm_exec_compute_pools
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_compute_pools dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d749b9a7d9689426bffafe20ee7ab46ce199ffbb
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75254610"
---
# <a name="sysdm_exec_compute_pools-transact-sql"></a>Sys. dm_exec_compute_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|nombre|`sysname`|Nombre del grupo de proceso. No admite valores NULL. Devuelve `default` para el grupo de proceso predeterminado. |
|compute_pool_id|`int`|Identificador único para el grupo. Clave para esta vista.|  
|location|`sysname`|Punto de conexión al controlador en un clúster de Big Data de SQL. No admite valores NULL. |

## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` el permiso.

## <a name="see-also"></a>Véase también

[¿Qué [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)]son ](../../big-data-cluster/big-data-cluster-overview.md)?
