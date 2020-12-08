---
title: SQL Server, objeto LogPool FreePool | Microsoft Docs
description: Obtenga información sobre el objeto de rendimiento SQLServer:LogPool FreePool, que proporciona contadores de estadísticas para el grupo libre dentro del grupo de registros.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:LogPool FreePool
ms.assetid: 8ffd569b-045f-4c3f-a473-4a491d6a1d80
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 8c41d49b9fb5e25381879a803b3b10963b13b8ba
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505659"
---
# <a name="sql-server-logpool-freepool-object"></a>SQL Server, objeto LogPool FreePool
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
El objeto de rendimiento **SQLServer:LogPool FreePool** proporciona contadores de estadísticas para el grupo libre dentro del grupo de registros.

En la siguiente tabla se describen los objetos de rendimiento **LogPool FreePool** de SQL Server.

|**Contadores de LogPool FreePool de SQL Server**|Descripción|  
|-------------|-----------------|  
|**Reabastecimientos de búferes disponibles por segundo**|Número de búferes asignados para reabastecer, por segundo.|
|**Longitud de lista de disponibles**|Longitud de la lista de disponibles.|

Hay una instancia del contador para cada categoría de grupo de registros.

## <a name="see-also"></a>Consulte también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)

