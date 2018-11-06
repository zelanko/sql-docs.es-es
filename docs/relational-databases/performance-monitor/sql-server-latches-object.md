---
title: Latches (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance-monitor
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d6622e43409d0e82b60cd2fc9cfe78909031c3d3
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51029717"
---
# <a name="sql-server-latches-object"></a>Latches (objeto de SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto **SQLServer:Latches** en Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar los bloqueos de recursos internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , denominados bloqueos temporales. La supervisión de los bloqueos temporales para determinar la actividad de los usuarios y el uso de los recursos puede ayudar a identificar puntos de congestión en el rendimiento.  
  
 En esta tabla se describen los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **de** .  
  
|Contadores de bloqueos temporales de SQL Server|Descripción|  
|---------------------------------|-----------------|  
|**Promedio de tiempo de espera para los bloqueos temporales (ms)**|Promedio de tiempo de espera de los bloqueos temporales (en milisegundos) para solicitudes de bloqueos temporales que tuvieron que esperar.|  
|**Base promedio de tiempo de espera de bloqueos temporales**|Exclusivamente para uso interno.| 
|**Esperas de bloqueos temporales/seg.**|Número de solicitudes de bloqueo temporal que no se concedieron inmediatamente.|  
|**Número de SuperLatches**|Número de bloqueos temporales que actualmente son SuperLatches.|  
|**Degradaciones de SuperLatch/seg.**|Número de SuperLatches degradados a bloqueos temporales normales en el último segundo transcurrido.|  
|**Ascensos a SuperLatch/seg.**|Número de bloqueos temporales ascendidos a SuperLatches en el último segundo transcurrido.|  
|**Tiempo total de espera de los bloqueos temporales (ms)**|Tiempo total de espera para bloqueos temporales (en milisegundos) de las solicitudes de bloqueos temporales en el último segundo.|  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
