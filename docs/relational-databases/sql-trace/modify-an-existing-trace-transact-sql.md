---
title: "Modificar un seguimiento existente (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "seguimientos [SQL Server], modificar"
  - "modificar seguimientos"
ms.assetid: 8792b43f-2510-44e3-9239-e73ad8227b89
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# Modificar un seguimiento existente (Transact-SQL)
  En este tema se describe cómo utilizar procedimientos almacenados para modificar un seguimiento existente.  
  
### Para modificar un seguimiento existente  
  
1.  Si el seguimiento ya se está ejecutando, ejecute **sp_trace_setstatus** con **@status = 0** para detener el seguimiento.  
  
2.  Para modificar los eventos del seguimiento, ejecute **sp_trace_setevent**, especificando los cambios a través de los parámetros. Los parámetros son, por este orden:  
  
    -   **@traceid** (Id. del seguimiento)  
  
    -   **@eventid** (Id. del evento)  
  
    -   **@columnid** (Id. de columna)  
  
    -   **@on** (ON)  
  
     Al modificar el parámetro **@on** , tenga presente su interacción con el parámetro **@columnid** :  
  
    |ON|Identificador de columna|Resultado|  
    |--------|---------------|------------|  
    |ON (**1**)|NULL|El evento se activa, se establece en ON. Se borran todas las columnas.|  
    ||NOT NULL|La columna se activa, se establece en ON, para el evento especificado.|  
    |OFF (**0**)|NULL|El evento se desactiva, se establece en OFF. Se borran todas las columnas.|  
    ||NOT NULL|La columna se desactiva, se establece en OFF, para el evento especificado.|  
  
> [!IMPORTANT]  
>  A diferencia de los procedimientos almacenados normales, los parámetros de todos los procedimientos almacenados del [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] (**sp_trace_*xx***) deben escribirse de forma precisa y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devuelve un error.  
  
## Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de SQL Server Profiler &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)  
  
  