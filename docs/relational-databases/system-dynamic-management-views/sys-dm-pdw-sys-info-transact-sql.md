---
title: sys.dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: ad7311759e2ea38f5b9b375785b7f035d1dcdbfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821523"
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Proporciona un conjunto de contadores de nivel de dispositivo que reflejan la actividad general en el dispositivo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|Número de sesiones actualmente en el sistema.|de 0 a max_active_sessions (ver abajo).|  
|idle_sessions|**int**|Número de sesiones está inactivas.||  
|active_requests|**int**|Número de solicitudes activas que se está ejecutando actualmente.||  
|queued_requests|**int**|Número de solicitudes actualmente en cola.||  
|active_loads|**int**|Número de cargas en ejecución actualmente en el sistema.||  
|queued_loads|**int**|Número de cargas en cola de espera de ejecución.||  
|active_backups|**int**|Número de copias de seguridad que se está ejecutando actualmente.||  
|active_restores|**int**|Número de copia de seguridad restauraciones que se está ejecutando actualmente.||  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de almacenamiento de datos en paralelo y SQL Data Warehouse &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
