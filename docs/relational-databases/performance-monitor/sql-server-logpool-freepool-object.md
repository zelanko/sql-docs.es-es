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
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b3ffe8512adc1fd21bcf33741d0a10db058d5752
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457729"
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

