---
title: Supervisión del uso de la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c8d7dc9fdf5a6cd6e52261c0d2327676db79508c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63239140"
---
# <a name="monitor-memory-usage"></a>Supervisar el uso de la memoria
  Supervise una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] periódicamente para confirmar que la utilización de la memoria se encuentra dentro de los intervalos normales.  
  
 Para supervisar las condiciones de memoria insuficiente, utilice los contadores de objetos siguientes:  
  
-   **Memoria: Bytes disponibles**  
  
-   **Memoria: Páginas/s**  
  
 El contador **Bytes disponibles** indica en bytes la memoria disponible actualmente para procesos. El contador **Páginas/s** indica el número de páginas que se han recuperado del disco debido a errores de página no recuperables o que se han escrito en disco para liberar espacio en el espacio de trabajo debido a errores de página.  
  
 Un valor bajo en el contador **Bytes disponibles** puede indicar una escasez general de memoria en el equipo o que un programa no está liberando memoria. Un valor alto en el contador **Páginas/s** puede indicar una paginación excesiva. Monitor del **memoria: Errores de página/s** para asegurarse de que la actividad del disco no está causada por la paginación.  
  
 Una tasa baja de paginación (y por tanto, de errores de página) es normal, incluso si el equipo tiene mucha memoria disponible. El Administrador de memoria virtual (VMM) de Microsoft Windows sustrae páginas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y otros procesos a medida que recorta los tamaños del espacio de trabajo para estos procesos, lo que suele provocar errores de página. Para determinar si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otro proceso son la causa de la paginación excesiva, supervise el **proceso: Errores de página/s** para la instancia del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener más información acerca de cómo solucionar la paginación excesiva, vea la documentación del sistema operativo Windows.  
  
## <a name="isolating-memory-used-by-sql-server"></a>Aislar la memoria que utiliza SQL Server  
 De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambia dinámicamente sus necesidades de memoria según los recursos del sistema disponibles. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita más memoria, consulta el sistema operativo para determinar si hay memoria física disponible y la utiliza. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no necesita la memoria que tiene asignada actualmente, la libera para el sistema operativo. En todo caso, el uso dinámico de la memoria puede anularse mediante las opciones de configuración de servidor **minservermemory**y **maxservermemory** . Para obtener más información, vea el documento sobre las [opciones de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
 Para supervisar la cantidad de memoria que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , examine los siguientes contadores de rendimiento:  
  
-   **Proceso: espacio de trabajo**  
  
-   **SQL Server: Administrador de búfer: frecuencia de aciertos de caché del búfer**  
  
-   **SQL Server: Administrador de búfer: páginas de base de datos**  
  
-   **SQL Server: Administrador de memoria: memoria total del servidor (KB)**  
  
 El contador **Espacio de trabajo** muestra la cantidad de memoria que usa un proceso. Si este número es constantemente inferior a la cantidad de memoria establecida en las opciones del servidor **min server memory** y **max server memory** , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para utilizar más memoria de la que necesita.  
  
 El contador **Frecuencia de aciertos de caché del búfer** es específico de la aplicación. Sin embargo, es preferible un porcentaje del 90% o superior. Agregue más memoria hasta que el valor sea superior al 90%, lo que indica que se ha atendido más del 90% de todas las solicitudes de información de la caché de datos.  
  
 Si el valor del contador **Memoria total del servidor (KB)** siempre es alto en comparación con la cantidad de memoria física del equipo, puede que indique que se necesita más memoria.  
  
## <a name="determining-current-memory-allocation"></a>Determinar la asignación de memoria actual  
 La consulta siguiente devuelve información acerca de la memoria asignada actual.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
