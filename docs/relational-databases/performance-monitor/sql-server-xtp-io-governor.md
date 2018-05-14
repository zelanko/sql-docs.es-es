---
title: SQL Server XTP IO Governor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: 2
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: c370bb68474c29d04615316ff7782ee1d532a561
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-xtp-io-governor"></a>SQL Server XTP IO Governor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El objeto de rendimiento SQL Server XTP IO Governor contiene contadores relacionados con el regulador de frecuencia de E/S OLPT en memoria.

En esta tabla se describen los contadores de **SQL Server XTP IO Governor** .

|Contador|Description|  
|-------------|-----------------|  
|**Esperas de créditos por segundo insuficientes**|Número de esperas debido a créditos insuficientes en los objetos de frecuencia (por segundo).|
|**E/S emitidas por segundo**|Número de E/S emitidas por segundo por los subprocesos de vaciado.|
|**Bloqueos de registro por segundo**|Número de bloqueos de registro procesados por el controlador por segundo.|
|**Ranuras de crédito perdidas**|Número de ranuras de crédito perdidas debido a la espera de créditos de objeto de frecuencia.|
|**Esperas por segundo de objetos de frecuencia obsoletos**|Número de esperas debido a objetos de frecuencia obsoletos (por segundo).|
|**Objetos de frecuencia totales publicados**|Número total de objetos de frecuencia publicados.|
 

## <a name="see-also"></a>Ver también  
[Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)
