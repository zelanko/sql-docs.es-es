---
title: Sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- sys.dm_resource_governor_external_resource_pool_affinity_TSQL
- dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_resource_governor_external_resource_pool_affinity
- dm_resource_governor_external_resource_pool_affinity
ms.assetid: e32fac49-5161-47c0-8540-af3fe730c00c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02ec95d318825c1759067455b62f3dae6a86c184
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053329"
---
# <a name="sysdm_resource_governor_external_resource_pool_affinity-transact-sql"></a>Sys. dm_resource_governor_external_resource_pool_affinity (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] y [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Devuelve información de afinidad de CPU acerca de la configuración actual del grupo de recursos externos.
  
|Nombre de la columna|Tipo de datos|Descripción|
|----------------|---------------|-----------------|
|pool_id|**int**|IDENTIFICADOR del grupo de recursos externos. No admite valores NULL.|
|processor_group|**smallint**|Identificador del grupo de procesadores lógicos de Windows. No admite valores NULL.|
|cpu_mask|**BIGINT**|Máscara binaria que representa las CPU asociadas a este grupo. No admite valores NULL.|
  
## <a name="remarks"></a>Observaciones

Los grupos creados con una afinidad de `AUTO` no aparecen en esta vista porque no tienen afinidad. Para obtener más información, vea [crear un grupo de recursos externos &#40;Transact-sql&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md) y [modificar el grupo de recursos externos &#40;instrucciones de transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md) .

## <a name="permissions"></a>Permisos

Requiere el permiso `VIEW SERVER STATE`.

## <a name="see-also"></a>Consulte también

[Regulación de recursos para machine learning en SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Sys. dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md)

[Opción de configuración de servidor Scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
