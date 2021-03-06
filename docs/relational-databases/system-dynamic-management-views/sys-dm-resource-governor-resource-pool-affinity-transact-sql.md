---
description: sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
title: Sys. dm_resource_governor_resource_pool_affinity (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_resource_pool_affinity_TSQL
- sys.dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity
- dm_resource_governor_resource_pool_affinity_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_resource_pool_affinity
- sys.dm_resource_governor_resource_pool_affinity
ms.assetid: a197ec19-a2ba-44f5-a4f2-3eee33ebd77d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c304b552dfbf09786af4c7d61edc64c99b004adc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546542"
---
# <a name="sysdm_resource_governor_resource_pool_affinity-transact-sql"></a>sys.dm_resource_governor_resource_pool_affinity (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Realiza el seguimiento de la afinidad del grupo de recursos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Nombre de Colmn|Tipo de datos|Descripción|  
|----------------|---------------|-----------------|  
|Pool_id|**int**|Identificador del grupo de recursos. No admite valores NULL.|  
|Processor_group|**smallint**|Identificador del grupo de procesadores lógicos de Windows. No admite valores NULL.|  
|Scheduler_mask|**bigint**|Máscara binaria que representa los programadores asociados a este grupo. No admite valores NULL.|  
  
## <a name="remarks"></a>Observaciones  
 Los grupos creados con la afinidad AUTO no aparecerán en esta vista porque no tienen ninguna afinidad. Para obtener más información, vea [Create Resource pool &#40;Transact-sql&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md) y [ALTER Resource Pool &#40;transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md) instrucciones.  
  
## <a name="see-also"></a>Consulte también  
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
