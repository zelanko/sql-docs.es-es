---
title: Almacenamiento de XTP de SQL Server | Microsoft Docs
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
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ca13381f6cc2d2b9af6286f28d25791522118a72
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-xtp-storage"></a>XTP Storage de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El objeto de rendimiento Almacenamiento de XTP de SQL Server contiene contadores relacionados con el almacenamiento en disco para OLTP en memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En esta tabla se describen los contadores de **Almacenamiento de XTP de SQL Server** .  
  
|Contador|Descripción|  
|-------------|-----------------|  
|**Checkpoints Closed**|Número de puntos de comprobación cerrados realizados por el agente en línea.|  
|**Checkpoints Completed**|Número de puntos de comprobación procesados por el subproceso de punto de comprobación sin conexión.|  
|**Core Merges Completed**|Número de mezclas básicas completadas por el subproceso de trabajo de mezcla. Todavía será necesario instalar estas mezclas.|  
|**Merge Policy Evaluations**|Número de evaluaciones de directivas de mezcla desde que el servidor se inició.|  
|**Merge Requests Outstanding**|Número de solicitudes de mezcla pendientes desde que el servidor se inició.|  
|**Merges Abandoned**|Número de mezclas abandonadas debido a un error.|  
|**Merges Installed**|Número de mezclas instaladas correctamente.|  
|**Total Files Merged**|Número total de archivos de origen mezclados. Este número se puede usar para determinar el número promedio de archivos de origen de la mezcla.|  
  
## <a name="see-also"></a>Vea también  
 [Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  

