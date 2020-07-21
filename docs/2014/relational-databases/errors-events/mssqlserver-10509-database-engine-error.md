---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 566d57843eaeafe02f7620c019aa6fbccdebd300
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552400"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10509|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_INVALID_STMT|  
|Texto del mensaje|No se puede crear la guía de plan '%.\*ls' porque la instrucción especificada por `@stmt` o `@statement_start_offset` contiene un error de sintaxis o es ilegible para una guía de plan. Especifique una sola instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] válida o una posición inicial válida de la instrucción en el lote. Para obtener una posición inicial válida, consulte la columna statement_start_offset de la función de administración dinámica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicación  
 La instrucción especificada por `@stmt` o `@statement_start_offset` contiene un error de sintaxis o es ilegible para una guía de plan.  
  
## <a name="user-action"></a>Acción del usuario  
 Especifique una sola instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] válida o una posición inicial válida de la instrucción en el lote. Para obtener una posición inicial válida, consulte la columna statement_start_offset de la función de administración dinámica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Consulte también  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guías de plan](../performance/plan-guides.md)   
 [Sys. dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
