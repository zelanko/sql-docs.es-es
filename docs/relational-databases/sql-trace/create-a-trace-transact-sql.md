---
title: Creación de un seguimiento guardado (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], example
- traces [SQL Server], creating
ms.assetid: 79dd4254-e3c6-467a-bb6f-f99e51757e99
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d872268d1ae879f46667f133f184264d9c3b8e49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751046"
---
# <a name="create-a-trace-transact-sql"></a>Crear un seguimiento (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe el modo de utilizar procedimientos almacenados para crear un seguimiento.  
  
### <a name="to-create-a-trace"></a>Para crear un seguimiento  
  
1.  Ejecute **sp_trace_create** con los parámetros necesarios para crear un seguimiento nuevo. El nuevo seguimiento estará en estado de detención (el*estado* es **0**).  
  
2.  Ejecute **sp_trace_setevent** con los parámetros necesarios para seleccionar los eventos y las columnas de las que va a realizar un seguimiento.  
  
3.  Opcionalmente, ejecute **sp_trace_setfilter** para establecer un filtro o una combinación de filtros.  

     **sp_trace_setevent** y **sp_trace_setfilter** solo se pueden ejecutar en seguimientos existentes que estén detenidos.  
  
    > [!IMPORTANT]  
    >  A diferencia de los procedimientos almacenados normales, los parámetros de todos los procedimientos almacenados de SQL Server Profiler (<strong>sp_trace_*xx*</strong>) tienen establecimiento inflexible de tipos y no admiten la conversión de tipos de datos automática. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devuelve un error.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se muestra la forma de crear un seguimiento con [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se divide en tres secciones: crear el seguimiento, rellenar el archivo de seguimiento y detener el seguimiento. Personalice el seguimiento agregando los eventos que desee seguir. Para obtener la lista de eventos y columnas, vea [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
 En el código siguiente se crea un seguimiento, se agregan los eventos al seguimiento y, a continuación, se inicia el seguimiento:  
  
```  
DECLARE @RC int, @TraceID int, @on BIT  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\SampleTrace'  
  
-- Select the return code to see if the trace creation was successful.  
SELECT RC = @RC, TraceID = @TraceID  
  
-- Set the events and data columns you need to capture.  
SELECT @on = 1  
  
-- 10 is RPC:Completed event. 1 is TextData column.   
EXEC sp_trace_setevent @TraceID, 10, 1, @on   
-- 13 is SQL:BatchStarting, 11 is LoginName  
EXEC sp_trace_setevent @TraceID, 13, 11, @on   
-- 13 is SQL:BatchStarting, 14 is StartTime  
EXEC sp_trace_setevent @TraceID, 13, 14, @on   
-- 12 is SQL:BatchCompleted, 15 is EndTime  
EXEC sp_trace_setevent @TraceID, 12, 15, @on   
-- 13 is SQL:BatchStarting, 1 is TextData  
EXEC sp_trace_setevent @TraceID, 13, 1, @on   
  
-- Set any filter. Not provided in this example  
--EXEC sp_trace_setfilter 1, 10, 0, 6, N'%Profiler%'  
  
-- Start Trace (status 1 = start)  
EXEC @RC = sp_trace_setstatus @TraceID, 1  
GO  
  
```  
  
## <a name="example"></a>Ejemplo  
 Ahora que se ha creado el seguimiento y se ha iniciado, ejecute el código siguiente para rellenarlo con actividad.  
  
```  
SELECT * FROM master.sys.databases  
GO  
SELECT * FROM ::fn_trace_getinfo(default)  
GO  
  
```  
  
## <a name="example"></a>Ejemplo  
 Se puede detener el seguimiento y reiniciar en cualquier momento. En este ejemplo, ejecute el código siguiente para detener el seguimiento, cerrarlo y eliminar su definición.  
  
```  
DECLARE @TraceID int  
-- Populate a variable with the trace_id of the current trace  
SELECT  @TraceID = TraceID FROM ::fn_trace_getinfo(default) WHERE VALUE = N'C:\SampleTrace.trc'  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2  
  
```  
  
## <a name="example"></a>Ejemplo  
 Para examinar el archivo de seguimiento, abra el archivo SampleTrace.trc mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)  
  
  
