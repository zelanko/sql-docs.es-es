---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b026dd0a0b9ecfc252947874b746cd5c18593f47
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68043679"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10535|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|PG_NO_PLAN|  
|Texto del mensaje|No se puede crear la guía de plan '%.*ls' porque no se encontró un plan en la memoria caché de plan que corresponda al identificador de plan especificado. Especifique el identificador de un plan almacenado en caché. Para ver una lista de identificadores de planes almacenados en caché, consulte la vista de administración dinámica sys.dm_exec_query_stats.|  
  
## <a name="explanation"></a>Explicación  
No se encontró un plan en la memoria caché de plan que corresponda al identificador de plan especificado.  
  
## <a name="user-action"></a>Acción del usuario  
Especifique el identificador de un plan almacenado en caché. Para ver una lista de identificadores de planes almacenados en caché, consulte la vista de administración dinámica sys.dm_exec_query_stats.  
  
## <a name="see-also"></a>Consulte también  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
