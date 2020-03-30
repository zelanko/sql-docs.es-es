---
title: Errores y advertencias (categoría de eventos)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4832910f00322875c334e16df77975a33106d214
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "74056423"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Errores y advertencias (categoría de eventos del motor de base de datos)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La categoría de eventos **Errores y advertencias** contiene eventos generales de errores y advertencias.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Attention (clase de eventos)](../../relational-databases/event-classes/attention-event-class.md)|Indica que se ha producido un evento **Attention** .|  
|[Background Job Error (clase de eventos)](../../relational-databases/event-classes/background-job-error-event-class.md)|Indica que un trabajo en segundo plano ha terminado de forma anómala.|  
|[Bitmap Warning (clase de eventos)](../../relational-databases/event-classes/bitmap-warning-event-class.md)|Indica que el filtrado de mapas de bits se ha deshabilitado en una consulta.|  
|[Blocked Process Report (clase de eventos)](../../relational-databases/event-classes/blocked-process-report-event-class.md)|Indica que una tarea ha estado bloqueada durante más tiempo del especificado.|  
|[CPU Threshold Exceeded (clase de eventos)](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)|Indica que el regulador de recursos detecta una consulta que supera el umbral de la CPU especificado.|  
|[ErrorLog (clase de eventos)](../../relational-databases/event-classes/errorlog-event-class.md)|Indica que se han registrado eventos de error en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[EventLog (clase de eventos)](../../relational-databases/event-classes/eventlog-event-class.md)|Indica que se han registrado eventos en el registro de eventos de Windows.|  
|[Exception (clase de eventos)](../../relational-databases/event-classes/exception-event-class.md)|Indica que se ha producido una excepción en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Exchange Spill (clase de eventos)](../../relational-databases/event-classes/exchange-spill-event-class.md)|Indica que los búferes de comunicaciones de un plan de consulta paralelo se han escrito en la base de datos tempdb.|  
|[Execution Warnings (clase de eventos)](../../relational-databases/event-classes/execution-warnings-event-class.md)|Indica que se produjeron advertencias de concesión de memoria durante la ejecución de una instrucción o procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Hash Warning (clase de eventos)](../../relational-databases/event-classes/hash-warning-event-class.md)|Indica que se ha producido una recursividad hash o un salida hash durante una operación de hash.|  
|[Missing Column Statistics (clase de eventos)](../../relational-databases/event-classes/missing-column-statistics-event-class.md)|Indica que no están disponibles las estadísticas de columna que podrían haber resultado útiles para el optimizador.|  
|[Missing Join Predicate (clase de eventos)](../../relational-databases/event-classes/missing-join-predicate-event-class.md)|Indica que se está ejecutando una consulta que no tiene ningún predicado de combinación.|  
|[Sort Warnings (clase de eventos)](../../relational-databases/event-classes/sort-warnings-event-class.md)|Indica que las operaciones de orden no caben en la memoria.|  
|[User Error Message (clase de eventos)](../../relational-databases/event-classes/user-error-message-event-class.md)|Muestra mensajes de error que ve el usuario.|  
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
