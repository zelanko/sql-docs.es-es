---
title: Sys.dm_pdw_os_performance_counters (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 0673a8f8-8bed-41eb-8959-a9e3e9e03a65
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0b4b346df5211f91519accf3c81374d0ab7302ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwosperformancecounters-transact-sql"></a>Sys.dm_pdw_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información sobre los contadores de rendimiento de Windows para los nodos en [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|El identificador del nodo que contiene el contador.<br /><br /> pdw_node_id y Nombre_contador forman la clave para esta vista.|Vea node_id en [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|counter_name|**nvarchar(255)**|Nombre del contador de rendimiento de Windows.||  
|counter_category|**nvarchar(255)**|Nombre de categoría de contador de rendimiento de Windows.||  
|nombre_instancia|**nvarchar(255)**|Nombre de la instancia específica del contador.||  
|counter_value|**Decimal(38,10)**|Valor actual del contador.||  
|last_update_time|**Datetime2(3)**|Marca de tiempo de la última vez que se actualizó el valor.||  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
