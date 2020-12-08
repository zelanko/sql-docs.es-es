---
title: Objeto SQL Server, Batch Resp Statistics | Microsoft Docs
description: Obtenga información sobre el objeto de rendimiento SQLServer:Batch Resp Statistics, que proporciona contadores para hacer un seguimiento de los tiempos de respuesta del proceso por lotes de SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: acd7dc7b853c600b743d9791a3bade6ce8970a41
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505884"
---
# <a name="sql-server-batch-resp-statistics-object"></a>Objeto SQL Server, Batch Resp Statistics
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
El objeto de rendimiento **SQLServer:Batch Resp Statistics** proporciona contadores para hacer seguimiento de los tiempos de respuesta del proceso por lotes de SQL Server.

En la tabla siguiente se describen los objetos de rendimiento **Batch Resp Statistics** de SQL Server.


|**Contadores de SQL Server Batch Resp Statistics**|Descripción|  
|-------------|-----------------|  
|**Lotes >=000000 ms y \<000001 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 0 ms pero menor que 1 ms|
|**Lotes >=000001 ms y \<000002 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 1 ms pero menor que 2 ms|
|**Lotes >=000002 ms y \<000005 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 2 ms pero menor que 5 ms|
|**Lotes >=000005 ms y \<000010 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 5 ms pero menor que 10 ms|
|**Lotes >=000010 ms y \<000020 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 10 ms pero menor que 20 ms|
|**Lotes >=000020 ms y \<000050 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 20 ms pero menor que 50 ms|
|**Lotes >=000050 ms y \<000100 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 50 ms pero menor que 100 ms|
|**Lotes >=000100 ms y \<000200 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 100 ms pero menor que 200 ms|
|**Lotes >=000200 ms y \<000500 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 200 ms pero menor que 500 ms|
|**Lotes >=000500 ms y \<001000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 500 ms pero menor que 1000 ms|
|**Lotes >=001000 ms y \<002000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 1000 ms pero menor que 2000 ms|
|**Lotes >=002000 ms y \<005000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 2000 ms pero menor que 5000 ms|
|**Lotes >=005000 ms y \<010000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 5000 ms pero menor que 10 000 ms|
|**Lotes >=010000 ms y \<020000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 10 000 ms pero menor que 20 000 ms|
|**Lotes >=020000 ms y \<050000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 20 000 ms pero menor que 50 000 ms|
|**Lotes >=050000 ms y \<100000 ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 50 000 ms pero menor que 100 000 ms| 
|**Batches >=100000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 100 000 ms| 

Cada contador del objeto contiene las instancias siguientes:  
  
|Elemento|Descripción|  
|----------|-----------------|  
|**CPU Time:Requests**|Número de solicitudes en función del tiempo de la CPU.|  
|**CPU Time:Total(ms)**|Tiempo total que la solicitud dedica al lote.|  
|**Elapsed Time:Requests**|Número de solicitudes en función del tiempo transcurrido.|  
|**Elapsed Time:Total(ms)**|Tiempo transcurrido del lote.|  

## <a name="see-also"></a>Consulte también
[Plan Cache (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
