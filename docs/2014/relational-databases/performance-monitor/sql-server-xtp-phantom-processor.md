---
title: Procesador fantasma de XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 14158b7097427b6704cf5e747fa998a11217ecd6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016787"
---
# <a name="xtp-phantom-processor"></a>Procesador fantasma de XTP
  El objeto de rendimiento Procesador fantasma de XTP contiene contadores relacionados con el subsistema de procesamiento fantasma del motor de XTP. Este componente es responsable de detectar filas fantasma en transacciones que se ejecutan en el nivel de aislamiento SERIALIZABLE.  
  
 En esta tabla se describen los contadores de **Procesador fantasma de XTP** .  
  
|Contador|Descripción|  
|-------------|-----------------|  
|**Reintentos de recorrido de esquinas sucias/s (emitidos por el fantasma)**|Número de reintentos de recorrido debido a conflictos de escritura durante los rastreos de esquinas sucias emitidos por el procesador fantasma (en promedio), por segundo. Es un contador de nivel muy bajo, no está pensado para uso de los clientes.|  
|**Filas fantasma expiradas quitadas/s**|Número de filas expiradas quitadas mediante recorridos fantasma (en promedio), por segundo.|  
|**Filas fantasma expiradas tocadas/s**|Número de filas expiradas tocadas por recorridos fantasma (en promedio), por segundo.|  
|**Filas fantasma que van a expirar tocadas/s**|Número de filas que van a expirar tocadas por recorridos fantasma (en promedio), por segundo.|  
|**Filas fantasma tocadas/s**|Número de filas tocadas por recorridos fantasma (en promedio), por segundo.|  
|**Recorridos fantasma iniciados/s**|Número de recorridos fantasma iniciados (en promedio), por segundo.|  
  
## <a name="see-also"></a>Consulte también  
 [Contadores de rendimiento de OLTP &#40;en memoria&#41;](../../integration-services/performance/performance-counters.md)  
  
  
