---
title: Procesador fantasma de XTP | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: 4
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bc489c0fc5be77e8dfaf2d2ea11a10515ec460e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114016"
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
  
## <a name="see-also"></a>Vea también  
 [XTP &#40;OLTP en memoria&#41; contadores de rendimiento](../../integration-services/performance/performance-counters.md)  
  
  