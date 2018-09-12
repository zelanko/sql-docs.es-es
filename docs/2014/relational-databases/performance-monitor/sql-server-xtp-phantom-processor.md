---
title: Procesador fantasma de XTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
caps.latest.revision: 4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 063fe5925c67e75381c4c97d17b5d7eba2125dfb
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810671"
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
 [XTP &#40;OLTP en memoria&#41; los contadores de rendimiento](../../integration-services/performance/performance-counters.md)  
  
  
