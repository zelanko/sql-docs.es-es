---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 419b45c688f755d6e5f7cf86154ce6cc527fc6ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761663"
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
  
