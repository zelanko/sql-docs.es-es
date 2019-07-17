---
title: Iniciar un seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, stopping traces
- pausing traces
- Profiler [SQL Server Profiler], stopping traces
- Profiler [SQL Server Profiler], starting traces
- traces [SQL Server], starting
- SQL Server Profiler, pausing traces
- traces [SQL Server], stopping
- Profiler [SQL Server Profiler], pausing traces
- traces [SQL Server], pausing
- SQL Server Profiler, starting traces
- stopping traces
- starting traces
ms.assetid: aeeb38eb-229a-4c8b-ad66-57e9ce45fb6a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1c53c039d6194edbc37438ef30ac4fef0113ae87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211038"
---
# <a name="start-a-trace"></a>Iniciar un seguimiento
  Una vez definida un nuevo seguimiento o creada una plantilla mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], puede iniciar, pausar o detener la captura de datos con la nueva definición de seguimiento o plantilla.  
  
## <a name="starting-a-trace"></a>Iniciar un seguimiento  
 Si inicia un seguimiento y el origen definido es una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una cola para colocar temporalmente los eventos de servidor capturados.  
  
 Si utiliza el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para tener acceso a Seguimiento de SQL, al iniciar un seguimiento se abre una nueva ventana de seguimiento (si aún no hay ninguna abierta) y los datos se capturan inmediatamente.  
  
 Si se utilizan los procedimientos almacenados del sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] para tener acceso a Seguimiento de SQL, debe iniciar un seguimiento cada vez que se inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que los datos se capturen. Una vez iniciado el seguimiento, solo puede modificar el nombre de este.  
  
> [!NOTE]  
>  Si trabaja con seguimientos existentes, puede ver las propiedades, pero no modificarlas. Para modificar las propiedades, detenga o pause el seguimiento.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar un seguimiento automáticamente después de conectarse a un servidor &#40;SQL Server Profiler&#41;](start-a-trace-automatically-after-connecting-to-a-server-sql-server-profiler.md)   
 [Pausar un seguimiento &#40;SQL Server Profiler&#41;](pause-a-trace-sql-server-profiler.md)   
 [Detener un seguimiento &#40;SQL Server Profiler&#41;](stop-a-trace-sql-server-profiler.md)   
 [Borrar el contenido de una ventana de seguimiento &#40;SQL Server Profiler&#41;](clear-a-trace-window-sql-server-profiler.md)   
 [Ejecutar un seguimiento después de haberlo pausado o detenido &#40;SQL Server Profiler&#41;](run-a-trace-after-it-has-been-paused-or-stopped-sql-server-profiler.md)  
  
  
