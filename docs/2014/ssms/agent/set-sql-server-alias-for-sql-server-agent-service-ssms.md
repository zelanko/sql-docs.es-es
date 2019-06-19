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
ms.openlocfilehash: e6e3ecc4b125d226fc2cdf6dbe241e0ce017eae6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245936"
---
# <a name="set-a-trace-filter-transact-sql"></a>Establecer un filtro de seguimiento (Transact-SQL)
  En este tema se describe el modo de utilizar procedimientos almacenados para crear un filtro que solo recupere la información necesaria en un evento que se está trazando.  
  
### <a name="to-set-a-trace-filter"></a>Para establecer un filtro de seguimiento  
  
1.  Si el seguimiento ya se está ejecutando, ejecute **sp_trace_setstatus** con **@status = 0** para detener el seguimiento.  
  
2.  Ejecute **sp_trace_setfilter** para configurar el tipo de información que se debe recuperar para el evento objeto del seguimiento.  
  
> [!IMPORTANT]
>  A diferencia de los procedimientos almacenados normales, los parámetros de todos los procedimientos almacenados de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (<strong>sp_trace_*xx*</strong>) tienen establecimiento inflexible de tipos y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
## <a name="see-also"></a>Vea también  
 [Filtrar un seguimiento](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
