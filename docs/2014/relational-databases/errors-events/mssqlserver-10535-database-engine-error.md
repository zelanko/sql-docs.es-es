---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 68070291c5e7f50d423b74338dc1f6baeb9c6dfa
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554120"
---
# <a name="mssqlserver_10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
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
 [sp_create_plan_guide_from_handle &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
