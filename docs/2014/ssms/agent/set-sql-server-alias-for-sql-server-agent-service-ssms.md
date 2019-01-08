---
title: Establecer un filtro de seguimiento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 803acc60555c996a0556e456b8d31753506b43ab
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53205794"
---
# <a name="set-a-trace-filter-transact-sql"></a>Establecer un filtro de seguimiento (Transact-SQL)
  En este tema se describe el modo de utilizar procedimientos almacenados para crear un filtro que solo recupere la información necesaria en un evento que se está trazando.  
  
### <a name="to-set-a-trace-filter"></a>Para establecer un filtro de seguimiento  
  
1.  Si el seguimiento ya se está ejecutando, ejecute **sp_trace_setstatus** con **@status = 0** para detener el seguimiento.  
  
2.  Ejecute **sp_trace_setfilter** para configurar el tipo de información que se debe recuperar para el evento objeto del seguimiento.  
  
> [!IMPORTANT]
>  A diferencia de los procedimientos almacenados normales, los parámetros de todos los procedimientos almacenados del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (**sp_trace_* xx***) deben escribirse de forma precisa y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
## <a name="see-also"></a>Vea también  
 [Filtrar un seguimiento](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
