---
title: SQL Server, objeto Distribuidores de agente de memoria | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
caps.latest.revision: 4
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7cf0f0a0d8ef7f7e8dec4a7a743dbc25bc98bb8d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, objeto Distribuidores de agente de memoria
El objeto de rendimiento **SQLServer:Distribuidores de agente de memoria** proporciona contadores para estadísticas relacionadas con los distribuidores de agente de memoria.

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

## <a name="see-also"></a>Vea también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
