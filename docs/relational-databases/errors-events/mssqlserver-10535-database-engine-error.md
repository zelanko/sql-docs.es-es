---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8260ba1dd2ddde91d41a3b5fa72e56fab23efb27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver10535"></a>MSSQLSERVER_10535
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10535|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_PLAN|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' porque no se encontró un plan en la memoria caché de plan que corresponda al identificador de plan especificado. Especifique el identificador de un plan almacenado en caché. Para ver una lista de identificadores de planes almacenados en caché, consulte la vista de administración dinámica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicación  
No se encontró un plan en la memoria caché de plan que corresponda al identificador de plan especificado.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique el identificador de un plan almacenado en caché. Para ver una lista de identificadores de planes almacenados en caché, consulte la vista de administración dinámica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Ver también  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
