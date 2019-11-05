---
title: Sys. DM _ _cluster_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 05076a6b694ff5861c5a7862b1f8f913ddb67fd6
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536171"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>Sys. DM _ _cluster_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|name|`sysname`|Nombre del servicio expuesto externamente en un clúster de macrodatos de SQL. Identificador único para el extremo. Clave para esta vista. No admite valores NULL. |  
|description|`nvarchar(4000)`|Descripción del servicio. No admite valores NULL. |
|extremo|`sysname`|Dirección URL del extremo o atributo de conexión. No admite valores NULL. |
|protocol_desc|`sysname`|Descripción del Protocolo de extremo |

## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.

## <a name="see-also"></a>Vea también

Qué son [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)](.. /.. /big-data-cluster/big-data-cluster-overview.md)?
