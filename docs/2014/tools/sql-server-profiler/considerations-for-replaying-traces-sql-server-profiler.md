---
title: Consideraciones para reproducir seguimientos (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 32b6073a1149303187668e83e666b486d0789c6a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112861"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>Consideraciones para reproducir seguimientos (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] no puede reproducir los siguientes tipos de seguimientos:  
  
-   Seguimientos que contengan actividad de replicación transaccional y otra actividad del registro de transacciones. Estos eventos se omiten. Otros tipos de replicación no marcan el registro de transacciones, por lo que esto no los afecta.  
  
-   Seguimientos que contengan operaciones que incluyan identificadores únicos globales (GUID). Estos eventos se omiten.  
  
-   Seguimientos que contengan operaciones en las columnas **text**, **ntext**e **image** para los que se haya usado la utilidad **bcp** , las instrucciones BULK INSERT, READTEXT, WRITETEXT y UPDATETEXT y operaciones de texto completo. Estos eventos se omiten.  
  
-   Seguimientos que contienen enlaces de sesión: procedimientos almacenados del sistema **sp_getbindtoken** y **sp_bindsession** . Estos eventos se omiten.  
  
> [!NOTE]  
>  Si no usa la plantilla de reproducción preconfigurada (**TSQL_Replay**), y no captura todos los datos necesarios, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] no reproducirá el seguimiento. Para más información, consulte [Replay Requirements](replay-requirements.md).  
  
 Para obtener información acerca de los permisos necesarios para reproducir un seguimiento, vea [Permissions Required to Run SQL Server Profiler](sql-server-profiler.md).  
  
## <a name="see-also"></a>Vea también  
 [bcp (utilidad)](../bcp-utility.md)   
 [Referencia de las clase de eventos de SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)   
 [sp_bindsession &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [READTEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/readtext-transact-sql)   
 [WRITETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/writetext-transact-sql)   
 [UPDATETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/updatetext-transact-sql)  
  
  
