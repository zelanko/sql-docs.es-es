---
title: Recolección de elementos no utilizados XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a064fec82054d434cc0ca577bc1dd013f3d16f2f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016840"
---
# <a name="xtp-garbage-collection"></a>Recolección de elementos no utilizados de XTP
  El objeto de rendimiento Recolección de elementos no utilizados de XTP contiene contadores relacionados con el recolector de elementos no utilizados del motor de XTP.  
  
 En esta tabla se describen los contadores de **Recolección de elementos no utilizados de XTP** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Contadores de rendimiento de OLTP &#40;en memoria&#41;](../../integration-services/performance/performance-counters.md)  
  
  
