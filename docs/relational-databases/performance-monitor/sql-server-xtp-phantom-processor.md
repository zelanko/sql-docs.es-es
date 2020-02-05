---
title: Procesador fantasma de XTP de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f9f7f51b2d0ede3bb49bb152ab08cbb2a7eb2732
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68114027"
---
# <a name="sql-server-xtp-phantom-processor"></a>Procesador fantasma de XTP de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El objeto de rendimiento Procesador fantasma de XTP de SQL Server contiene contadores relacionados con el subsistema de procesamiento fantasma del motor de OLTP en memoria. Este componente es responsable de detectar filas fantasma en transacciones que se ejecutan en el nivel de aislamiento SERIALIZABLE, así como de la validación de restricciones en escenarios de simultaneidad.  
  
 En esta tabla se describen los contadores de **Procesador fantasma de XTP de SQL Server** .  
  
|Contador|Descripción|  
|-------------|-----------------|  
|**Reintentos de recorrido de esquinas sucias/s (emitidos por el fantasma)**|Número de reintentos de recorrido debido a conflictos de escritura durante los rastreos de esquinas sucias emitidos por el procesador fantasma (en promedio), por segundo. Es un contador de nivel muy bajo, no está pensado para uso de los clientes.|  
|**Filas fantasma expiradas quitadas/s**|Número de filas expiradas quitadas mediante recorridos fantasma (en promedio), por segundo.|  
|**Filas fantasma expiradas tocadas/s**|Número de filas expiradas tocadas por recorridos fantasma (en promedio), por segundo.|  
|**Filas fantasma que van a expirar tocadas/s**|Número de filas que van a expirar tocadas por recorridos fantasma (en promedio), por segundo.|  
|**Filas fantasma tocadas/s**|Número de filas tocadas por recorridos fantasma (en promedio), por segundo.|  
|**Recorridos fantasma iniciados/s**|Número de recorridos fantasma iniciados (en promedio), por segundo.|  
  
## <a name="see-also"></a>Consulte también  
 [Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
