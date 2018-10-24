---
title: SQL Server, objeto Distribuidores de agente de memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: 546d5052c2b97b40b4f7e979c0447c947fdf487a
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906035"
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, objeto Distribuidores de agente de memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
El objeto de rendimiento **SQLServer:Distribuidores de agente de memoria** proporciona contadores para estadísticas relacionadas con los distribuidores de agente de memoria.

En la siguiente tabla se describen los objetos de rendimiento **Distribuidores de agente de memoria** de SQL Server.

|**Contadores de Distribuidores de agente de memoria de SQL Server**|Descripción|  
|-------------|-----------------|  
|**Beneficio interno**|Valor interno de memoria para la presión de recuento de entradas, en ms por página por ms, multiplicado por 10 000 millones y truncado en un entero.|
|**Tamaño de distribuidores de agente de memoria**|Tamaño del distribuidor, en páginas.|
|**Expulsiones periódicas (páginas)**|Número de páginas expulsadas del distribuidor de agente por la última expulsión periódica.|
|**Expulsiones de presión (páginas/s)**|Número de páginas por segundo expulsadas del distribuidor de agente por la presión de memoria|
|**Beneficio de simulación**|Valor de memoria para el distribuidor, en ms por página por ms, multiplicado por 10 000 millones y truncado en un entero.|
|**Tamaño de simulación**|Tamaño actual de la simulación de distribuidor, en páginas.|

Existe una instancia del contador para el grupo de búferes y el grupo de objetos de almacén de columnas.

## <a name="see-also"></a>Ver también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
