---
title: Sys. dm_pdw_wait_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cfb8d905-c34f-44de-9574-dde81e170916
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 2d5815783528b89716cc8bfb426ea7c1b274802e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088720"
---
# <a name="sysdm_pdw_wait_stats-transact-sql"></a>Sys. dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información relacionada con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el estado del sistema operativo relacionado con las instancias que se ejecutan en los distintos nodos. Para obtener una lista de los tipos de esperas y su descripción, vea [Sys. dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx).  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|IDENTIFICADOR del nodo al que hace referencia esta entrada.||  
|**wait_name**|**nvarchar(255)**|Nombre del tipo de espera.||  
|**max_wait_time**|**BIGINT**|Tiempo de espera máximo de este tipo de espera.||  
|**request_count**|**BIGINT**|Número de esperas pendientes de este tipo de espera.||  
|**signal_time**|**BIGINT**|Diferencia entre el momento en que se indicó el subproceso en espera y el momento en que empezó a ejecutarse.||  
|**completed_count**|**BIGINT**|Número total de esperas de este tipo completadas desde el último reinicio del servidor.||  
|**wait_time**|**BIGINT**|Tiempo de espera total para este tipo de espera en millisecons. Inclusivo de signal_time.||  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de administración dinámica de SQL Data Warehouse y almacenamiento de datos paralelos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [Sys. dm_pdw_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
