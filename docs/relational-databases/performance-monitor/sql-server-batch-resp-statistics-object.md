---
title: "Objeto SQL Server, Batch Resp Statistics | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQLServer:Batch Resp Statistics"
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
caps.latest.revision: 3
author: "dagiro"
ms.author: "v-dagir"
manager: "jhubbard"
caps.handback.revision: 3
---
# Objeto SQL Server, Batch Resp Statistics
El objeto de rendimiento **SQLServer:Batch Resp Statistics** proporciona contadores para hacer seguimiento de los tiempos de respuesta del proceso por lotes de SQL Server.

En la tabla siguiente se describen los objetos de rendimiento **Batch Resp Statistics** de SQL Server.


|**Contadores de SQL Server Batch Resp Statistics**|Description|  
|-------------|-----------------|  
|**Batches >=000000ms & \<000001ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 0 ms pero menor que 1 ms|
|**Batches >=000001ms & \<000002ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 1 ms pero menor que 2 ms|
|**Batches >=000002ms & \<000005ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 2 ms pero menor que 5 ms|
|**Batches >=000005ms & \<000010ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 5 ms pero menor que 10 ms|
|**Batches >=000010ms & \<000020ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 10 ms pero menor que 20 ms|
|**Batches >=000020ms & \<000050ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 20 ms pero menor que 50 ms|
|**Batches >=000050ms & \<000100ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 50 ms pero menor que 100 ms|
|**Batches >=000100ms & \<000200ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 100 ms pero menor que 200 ms|
|**Batches >=000200ms & \<000500ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 200 ms pero menor que 500 ms|
|**Batches >=000500ms & \<001000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 500 ms pero menor que 1000 ms|
|**Batches >=001000ms & \<002000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 1000 ms pero menor que 2000 ms|
|**Batches >=002000ms & \<005000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 2000 ms pero menor que 5000 ms|
|**Batches >=005000ms & \<010000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 5000 ms pero menor que 10 000 ms|
|**Batches >=010000ms & \<020000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 10 000 ms pero menor que 20 000 ms|
|**Batches >=020000ms & \<050000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 20 000 ms pero menor que 50 000 ms|
|**Batches >=050000ms & \<100000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 50 000 ms pero menor que 100 000 ms| 
|**Batches >=100000ms**|Número de procesos por lotes de SQL que tienen un tiempo de respuesta mayor o igual a 100 000 ms| 

Cada contador del objeto contiene las instancias siguientes:  
  
|Elemento|Description|  
|----------|-----------------|  
|**CPU Time:Requests**|Tiempo que la CPU dedica a la solicitud.|  
|**CPU Time:Total(ms)**|Tiempo total que la solicitud dedica al lote.|  
|**Elapsed Time:Requests**|Tiempo transcurrido de la solicitud.|  
|**Elapsed Time:Total(ms)**|Tiempo transcurrido del lote.|  

## Vea también
[Plan Cache (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[Supervisar el uso de recursos (Monitor de sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  