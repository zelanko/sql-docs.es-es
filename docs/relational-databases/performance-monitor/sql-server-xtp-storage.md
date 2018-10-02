---
title: Almacenamiento de XTP de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 4070580b-880d-4f4c-abcc-626a4fe0c9a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ad892774f11ed4eab2f3809c0fce8805b268c107
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730123"
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
  
## <a name="see-also"></a>Ver también  
 [Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
