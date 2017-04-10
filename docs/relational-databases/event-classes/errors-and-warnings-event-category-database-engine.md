---
title: "Errores y advertencias (categor&#237;a de eventos del motor de base de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Errores y advertencias, categoría de eventos [SQL Server]"
  - "Clases de eventos de SQL Server, categoría de eventos de errores y advertencias"
  - "clases de eventos [SQL Server], categoría de eventos de errores y advertencias"
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
caps.latest.revision: 28
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 28
---
# Errores y advertencias (categor&#237;a de eventos del motor de base de datos)
  La categoría de eventos **Errores y advertencias** contiene eventos generales de errores y advertencias.  
  
## En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Attention (clase de eventos)](../../relational-databases/event-classes/attention-event-class.md)|Indica que se ha producido un evento **Attention** .|  
|[Background Job Error (clase de eventos)](../../relational-databases/event-classes/background-job-error-event-class.md)|Indica que un trabajo en segundo plano ha terminado de forma anómala.|  
|[Bitmap Warning (clase de eventos)](../../relational-databases/event-classes/bitmap-warning-event-class.md)|Indica que el filtrado de mapas de bits se ha deshabilitado en una consulta.|  
|[Blocked Process Report (clase de eventos)](../../relational-databases/event-classes/blocked-process-report-event-class.md)|Indica que una tarea ha estado bloqueada durante más tiempo del especificado.|  
|[Clase de eventos Umbral de la CPU superado](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)|Indica que el regulador de recursos detecta una consulta que supera el umbral de la CPU especificado.|  
|[ErrorLog (clase de eventos)](../../relational-databases/event-classes/errorlog-event-class.md)|Indica que se han registrado eventos de error en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[EventLog (clase de eventos)](../../relational-databases/event-classes/eventlog-event-class.md)|Indica que se han registrado eventos en el registro de eventos de Windows.|  
|[Exception (clase de eventos)](../../relational-databases/event-classes/exception-event-class.md)|Indica que se ha producido una excepción en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Exchange Spill (clase de eventos)](../../relational-databases/event-classes/exchange-spill-event-class.md)|Indica que los búferes de comunicaciones de un plan de consulta paralelo se han escrito en la base de datos tempdb.|  
|[Execution Warnings (clase de eventos)](../../relational-databases/event-classes/execution-warnings-event-class.md)|Indica que se produjeron advertencias de concesión de memoria durante la ejecución de una instrucción o procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Hash Warning (clase de eventos)](../../relational-databases/event-classes/hash-warning-event-class.md)|Indica que se ha producido una recursividad hash o un salida hash durante una operación de hash.|  
|[Missing Column Statistics (clase de eventos)](../../relational-databases/event-classes/missing-column-statistics-event-class.md)|Indica que no están disponibles las estadísticas de columna que podrían haber resultado útiles para el optimizador.|  
|[Missing Join Predicate (clase de eventos)](../../relational-databases/event-classes/missing-join-predicate-event-class.md)|Indica que se está ejecutando una consulta que no tiene ningún predicado de combinación.|  
|[Sort Warnings (clase de eventos)](../../relational-databases/event-classes/sort-warnings-event-class.md)|Indica que las operaciones de orden no caben en la memoria.|  
|[User Error Message (clase de eventos)](../../relational-databases/event-classes/user-error-message-event-class.md)|Muestra mensajes de error que ve el usuario.|  
  
## Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  