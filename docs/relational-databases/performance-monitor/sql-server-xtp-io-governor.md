---
title: SQL Server XTP IO Governor | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91e176fe-c838-44e9-b4fc-2814a0551ca3
caps.latest.revision: 2
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dad1b34551ae96587fafdf3f232ce96b33a96846
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
 

## <a name="see-also"></a>Vea también  
[Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)

