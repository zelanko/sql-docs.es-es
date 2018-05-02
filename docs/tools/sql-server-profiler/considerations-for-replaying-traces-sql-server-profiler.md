---
title: Consideraciones para reproducir seguimientos (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 076b34d06f7644b471dd16694c293baafdb3a8bc
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>Consideraciones para reproducir seguimientos (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] no puede reproducir los siguientes tipos de seguimientos:  
  
-   Seguimientos que contengan actividad de replicación transaccional y otra actividad del registro de transacciones. Estos eventos se omiten. Otros tipos de replicación no marcan el registro de transacciones, por lo que esto no los afecta.  
  
-   Seguimientos que contengan operaciones que incluyan identificadores únicos globales (GUID). Estos eventos se omiten.  
  
-   Seguimientos que contengan operaciones en las columnas **text**, **ntext**e **image** para los que se haya usado la utilidad **bcp** , las instrucciones BULK INSERT, READTEXT, WRITETEXT y UPDATETEXT y operaciones de texto completo. Estos eventos se omiten.  
  
-   Seguimientos que contienen enlaces de sesión: procedimientos almacenados del sistema **sp_getbindtoken** y **sp_bindsession** . Estos eventos se omiten.  
  
> [!NOTE]  
>  Si no usa la plantilla de reproducción preconfigurada (**TSQL_Replay**), y no captura todos los datos necesarios, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] no reproducirá el seguimiento. Para más información, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
 Para obtener información acerca de los permisos necesarios para reproducir un seguimiento, vea [Permissions Required to Run SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="see-also"></a>Ver también  
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [Referencia de las clase de eventos de SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [sp_bindsession &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindsession-transact-sql.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)   
 [WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)   
 [UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)  
  
  
