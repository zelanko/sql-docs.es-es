---
title: Establecer un filtro de seguimiento (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98d18b704ff407064cd18083b79f80f901d21903
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750930"
---
# <a name="set-a-trace-filter-transact-sql"></a>Establecer un filtro de seguimiento (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe el modo de utilizar procedimientos almacenados para crear un filtro que solo recupere la información necesaria en un evento que se está trazando.  
  
### <a name="to-set-a-trace-filter"></a>Para establecer un filtro de seguimiento  
  
1.  Si el seguimiento ya está en ejecución, ejecute **sp_trace_setstatus** y especifique `@status = 0` para detener el seguimiento.  
  
2.  Ejecute **sp_trace_setfilter** para configurar el tipo de información que se debe recuperar para el evento objeto del seguimiento.  

> [!IMPORTANT]  
>  A diferencia de los procedimientos almacenados normales, los parámetros de todos los procedimientos almacenados de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (**sp_trace\__xx_** ) tienen establecimiento inflexible de tipos y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devolverá un error.  
  
## <a name="see-also"></a>Consulte también  
 [Filtrar un seguimiento](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  
