---
description: Sys. dm_pdw_os_performance_counters (Transact-SQL)
title: Sys. dm_pdw_os_performance_counters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 08ef29f6fe47099bcbbdeb87fce0dfb5aa25a42a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474747"
---
# <a name="sysdm_pdw_os_performance_counters-transact-sql"></a>Sys. dm_pdw_os_performance_counters (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contiene información sobre los contadores de rendimiento de Windows para los nodos de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|IDENTIFICADOR del nodo que contiene el contador.<br /><br /> pdw_node_id y counter_name forman la clave de esta vista.|Vea node_id en [Sys. dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|counter_name|**nvarchar(255)**|Nombre del contador de rendimiento de Windows.||  
|counter_category|**nvarchar(255)**|Nombre de la categoría del contador de rendimiento de Windows.||  
|nombre_instancia|**nvarchar(255)**|Nombre de la instancia específica del contador.||  
|counter_value|**Decimal (38, 10)**|Valor actual del contador.||  
|last_update_time|**Datetime2 (3)**|Marca de tiempo de la última vez que se actualizó el valor.||  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
