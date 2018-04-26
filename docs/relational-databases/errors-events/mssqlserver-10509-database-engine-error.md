---
title: MSSQLSERVER_10509 | Microsoft Docs
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
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d3aa303297c00b122cb44a6dc4db75942a082164
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10509|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INVALID_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque la instrucción especificada por **@stmt** o **@statement_start_offset** contiene un error de sintaxis o es ilegible para una guía de plan. Especifique una sola instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] válida o una posición inicial válida de la instrucción en el lote. Para obtener una posición inicial válida, consulte la columna statement_start_offset de la función de administración dinámica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicación  
La instrucción especificada por **@stmt** o **@statement_start_offset** contiene un error de sintaxis o resulta ilegible para usarla en una guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique una sola instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] válida o una posición inicial válida de la instrucción en el lote. Para obtener una posición inicial válida, consulte la columna statement_start_offset de la función de administración dinámica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Ver también  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guías de plan](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
