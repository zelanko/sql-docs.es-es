---
title: "Recolección de elementos no utilizados de XTP de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84e7b0df9fdd52f6f67113b9dc019fc905a9aaff
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-garbage-collection"></a>Recolección de elementos no utilizados de XTP de SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  El objeto de rendimiento Recolección de elementos no utilizados de XTP de SQL Server contiene contadores relacionados con el recolector de elementos no utilizados del motor OLTP en memoria.  
  
 En esta tabla se describen los contadores de **Recolección de elementos no utilizados de XTP de SQL Server** .  
  
|Contador|Descripción|  
|-------------|-----------------|  
|**Reintentos de recorrido de esquinas sucias/s (emitidos por GC)**|Número de reintentos de recorrido debido a conflictos de escritura durante los rastreos de esquinas sucias emitidos por el recolector de elementos no utilizados (en promedio), por segundo. Es un contador de nivel muy bajo, no está pensado para uso de los clientes.|  
|**Elementos de trabajo principales de GC/s**|Número de elementos de trabajo procesados por el subproceso principal de GC.|  
|**Elemento de trabajo paralelo de GC/s**|Número de veces que un subproceso paralelo ha ejecutado un elemento de trabajo de GC.|  
|**Filas procesadas/s**|Número de filas procesadas por el recolector de elementos no utilizados (en promedio), por segundo.|  
|**Filas procesadas/s (primero en el cubo y quitadas)**|Número de filas procesadas por el recolector de elementos no utilizados que estaban primero en el depósito de hash correspondiente, y que se pudieron quitar inmediatamente (en promedio), por segundo.|  
|**Filas procesadas/s (primero en el cubo)**|Número de filas procesadas por el recolector de elementos no utilizados que estaban primero en el depósito de hash correspondiente (en promedio), por segundo.|  
|**Filas procesadas/s (marcadas para desvincular)**|Número de filas procesadas por el recolector de elementos no utilizados que ya estaban marcadas para desvincular (en promedio), por segundo.|  
|**Filas procesadas/s (no se necesita ningún rastreo)**|Número de filas procesadas por el recolector de elementos no utilizados que no necesitarán un rastreo de esquinas sucias (en promedio), por segundo.|  
|**Rastreo de filas expiradas quitadas/s**|Número de filas expiradas quitadas durante los rastreos de esquinas sucias (en promedio), por segundo.|  
|**Rastreo de filas expiradas tocadas/s**|Número de filas expiradas tocadas durante los rastreos de esquinas sucias (en promedio), por segundo.|  
|**Rastreo de filas que van a expirar tocadas/s**|Número de filas que van a expirar tocadas durante los rastreos de esquinas sucias (en promedio), por segundo.|  
|**Rastreo de filas tocadas/s**|Número de filas tocadas durante los rastreos de esquinas sucias (en promedio), por segundo.|  
|**Rastreo de recorridos iniciados/s**|Número de recorridos de rastreo de esquinas sucias iniciados (en promedio), por segundo.|  
  
## <a name="see-also"></a>Vea también  
 [Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  

