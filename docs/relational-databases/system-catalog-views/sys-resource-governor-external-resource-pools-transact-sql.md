---
title: Sys. resource_governor_external_resource_pools (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.resource_governor_external_resource_pools
- sys.resource_governor_external_resource_pools_TSQL
- resource_governor_external_resource_pools
- resource_governor_external_resource_pools_TSQL
helpviewer_keywords:
- sys.resource_governor_external_resource_pools
- resource_governor_external_resource_pools
ms.assetid: 75063e36-a91b-496f-9936-88f3d57bd447
author: stevestein
ms.author: sstein
ms.openlocfilehash: 379dae51b913fc02a16a562037776620b1e0433c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67904472"
---
# <a name="sysresource_governor_external_resource_pools-transact-sql"></a>Sys. resource_governor_external_resource_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] y [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Devuelve la configuración del grupo de recursos externos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]almacenado en. Cada fila de la vista determina la configuración de un grupo.
  
|Nombre de la columna|Tipo de datos|Descripción|
|-----------------|---------------|-----------------|
|pool_id|**int**|Identificador único del grupo de recursos de servidor. No admite valores NULL.<br /><br /> **Nota:** Se puede cambiar el nombre en el futuro.|
|name|**sysname**|Nombre del grupo de recursos de servidor. No admite valores NULL.|
|max_cpu_percent|**int**|Ancho banda de la CPU promedio máximo permitido para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. No admite valores NULL.|
|max_memory_percent|**int**|Porcentaje de la memoria total del servidor que puede utilizarse en las solicitudes en este grupo de recursos de servidor. No admite valores NULL. El máximo efectivo depende de los mínimos del grupo. Por ejemplo, max_memory_percent puede estar establecido en 100, pero el máximo efectivo es menor.|
|max_processes|**int**|Número máximo de procesos externos simultáneos. El valor predeterminado, 0, especifica que no hay límite. No admite valores NULL.|
|version|**BIGINT**|Número de versión interno.|
  
## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="see-also"></a>Consulte también

[Regulación de recursos para machine learning en SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Resource Governor vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)

[Sys. dm_resource_governor_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql.md)

[Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

[Sys. dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opción de configuración de servidor Scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
