---
title: SQL Server, objeto Distribuidores de agente de memoria | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
caps.latest.revision: "4"
author: dagiro
ms.author: v-dagir
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d86b986025348a829734d57625a0567041cd12d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, objeto Distribuidores de agente de memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] El objeto de rendimiento **SQLServer:Memory Broker Clerks** proporciona contadores para estadísticas relacionadas con los distribuidores de agente de memoria.

En la siguiente tabla se describen los objetos de rendimiento **Distribuidores de agente de memoria** de SQL Server.

|**Contadores de Distribuidores de agente de memoria de SQL Server**|Description|  
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
