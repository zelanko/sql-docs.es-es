---
title: sys.dm_pdw_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 686976b4-2d5d-4d64-bf12-56eba1dc59b1
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: e1fe45c9844346b96da561dc48786ffbed963d77
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwsysinfo-transact-sql"></a>sys.dm_pdw_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Proporciona un conjunto de contadores de nivel de dispositivo que reflejan la actividad general en el dispositivo.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|total_sessions|**int**|Número de sesiones actualmente en el sistema.|de 0 a max_active_sessions (ver abajo).|  
|idle_sessions|**int**|Número de sesiones actualmente inactivas.||  
|active_requests|**int**|Número de solicitudes activas que se está ejecutando actualmente.||  
|queued_requests|**int**|Número de solicitudes actualmente en cola.||  
|active_loads|**int**|Número de cargas en ejecución actualmente en el sistema.||  
|queued_loads|**int**|Número de cargas en cola que esperan la ejecución.||  
|active_backups|**int**|Número de copias de seguridad que se está ejecutando actualmente.||  
|active_restores|**int**|Número de restauración de copia de seguridad que está ejecutando actualmente.||  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
