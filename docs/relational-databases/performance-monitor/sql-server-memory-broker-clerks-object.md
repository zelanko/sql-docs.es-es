---
title: SQL Server, objeto Distribuidores de agente de memoria | Microsoft Docs
description: Obtenga información sobre el objeto de rendimiento SQLServer:Memory Broker Clerks, que proporciona contadores para estadísticas relacionadas con los distribuidores de agente de memoria.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 728a660b3737410e9f235cb8632cbf948f7bcf82
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458809"
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, objeto Distribuidores de agente de memoria
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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

## <a name="see-also"></a>Consulte también  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
