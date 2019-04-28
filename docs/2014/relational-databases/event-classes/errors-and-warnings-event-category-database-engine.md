---
title: Errores y advertencias (categoría de eventos del motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Errors and Warnings event category [SQL Server]
- SQL Server event classes, Errors and Warnings event category
- event classes [SQL Server], Errors and Warnings event category
ms.assetid: 249c19b5-af68-4433-80f6-337395176641
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b86b68b0e7273a275c8dd1bd00fe99a7c462a27d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62662631"
---
# <a name="errors-and-warnings-event-category-database-engine"></a>Errores y advertencias (categoría de eventos del motor de base de datos)
  La categoría de eventos **Errores y advertencias** contiene eventos generales de errores y advertencias.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Attention (clase de eventos)](attention-event-class.md)|Indica que se ha producido un evento **Attention** .|  
|[Background Job Error (clase de eventos)](background-job-error-event-class.md)|Indica que un trabajo en segundo plano ha terminado de forma anómala.|  
|[Bitmap Warning (clase de eventos)](bitmap-warning-event-class.md)|Indica que el filtrado de mapas de bits se ha deshabilitado en una consulta.|  
|[Blocked Process Report (clase de eventos)](blocked-process-report-event-class.md)|Indica que una tarea ha estado bloqueada durante más tiempo del especificado.|  
|[CPU Threshold Exceeded (clase de eventos)](cpu-threshold-exceeded-event-class.md)|Indica que el regulador de recursos detecta una consulta que supera el umbral de la CPU especificado.|  
|[ErrorLog (clase de eventos)](errorlog-event-class.md)|Indica que se han registrado eventos de error en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[EventLog (clase de eventos)](eventlog-event-class.md)|Indica que se han registrado eventos en el registro de eventos de Windows.|  
|[Exception (clase de eventos)](exception-event-class.md)|Indica que se ha producido una excepción en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Exchange Spill (clase de eventos)](exchange-spill-event-class.md)|Indica que los búferes de comunicaciones de un plan de consulta paralelo se han escrito en la base de datos tempdb.|  
|[Execution Warnings (clase de eventos)](execution-warnings-event-class.md)|Indica que se produjeron advertencias de concesión de memoria durante la ejecución de una instrucción o procedimiento almacenado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Hash Warning (clase de eventos)](hash-warning-event-class.md)|Indica que se ha producido una recursividad hash o un salida hash durante una operación de hash.|  
|[Missing Column Statistics (clase de eventos)](missing-column-statistics-event-class.md)|Indica que no están disponibles las estadísticas de columna que podrían haber resultado útiles para el optimizador.|  
|[Missing Join Predicate (clase de eventos)](missing-join-predicate-event-class.md)|Indica que se está ejecutando una consulta que no tiene ningún predicado de combinación.|  
|[Sort Warnings (clase de eventos)](sort-warnings-event-class.md)|Indica que las operaciones de orden no caben en la memoria.|  
|[User Error Message (clase de eventos)](user-error-message-event-class.md)|Muestra mensajes de error que ve el usuario.|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
