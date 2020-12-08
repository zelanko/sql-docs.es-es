---
title: Procesador fantasma de XTP de SQL Server | Microsoft Docs
description: Obtenga información sobre el objeto de rendimiento Procesador fantasma de XTP de SQL Server, que contiene contadores relacionados con el subsistema de procesamiento fantasma del motor de OLTP en memoria.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: c0547f8f93b548e7dcf51271e7c796bad52f46ad
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505479"
---
# <a name="sql-server-xtp-phantom-processor"></a>Procesador fantasma de XTP de SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
  
