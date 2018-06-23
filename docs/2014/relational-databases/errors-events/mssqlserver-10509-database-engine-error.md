---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fb203b703df342107384cf0c082917aea18c5f20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109245"
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10509|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INVALID_STMT|  
|Texto del mensaje|No se puede crear la Guía de plan ' %. \*ls' porque la instrucción especificada por `@stmt` o `@statement_start_offset` contiene un error de sintaxis o es ilegible para una guía de plan. Especifique una sola instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] válida o una posición inicial válida de la instrucción en el lote. Para obtener una posición inicial válida, consulte la columna statement_start_offset de la función de administración dinámica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicación  
 La instrucción especificada por `@stmt` o `@statement_start_offset` contiene un error de sintaxis o es ilegible para una guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique una sola instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] válida o una posición inicial válida de la instrucción en el lote. Para obtener una posición inicial válida, consulte la columna statement_start_offset de la función de administración dinámica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Vea también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
