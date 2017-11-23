---
title: Sys.dm_pdw_wait_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: dmv's
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2a567c103a0a2b3f3dac24accd8099d2bd85e80
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwwaitstats-transact-sql"></a>Sys.dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información relacionada con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estado del sistema operativo relacionados con instancias que se ejecutan en los distintos nodos. Para obtener una lista de tipos de esperas y sus descripciones, consulte [sys.dm_os_wait_stats](http://msdn.microsoft.com/en-us/library/ms179984\(v=sql.120\).aspx).  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|Identificador del nodo al que hace referencia esta entrada.||  
|**wait_name**|**nvarchar(255)**|Nombre del tipo de espera.||  
|**max_wait_time**|**bigint**|Tiempo de espera máximo de este tipo de espera.||  
|**request_count**|**bigint**|Número de esperas de este tipo pendiente de espera.||  
|**signal_time**|**bigint**|Diferencia entre el momento en que se indicó el subproceso en espera y el momento en que empezó a ejecutarse.||  
|**completed_count**|**bigint**|Número total de las esperas de este tipo completadas desde el último servidor de reinicio.||  
|**tiempoespera**|**bigint**|Tiempo de espera total para este tipo de espera en millisecons. Favorecer signal_time.||  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [Sys.dm_pdw_waits &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
