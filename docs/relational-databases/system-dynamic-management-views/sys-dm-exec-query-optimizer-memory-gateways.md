---
title: Sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL) | Microsoft Docs
description: Devuelve el estado actual de semáforos de recursos que se utiliza para acelerar la optimización de consultas simultáneas
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: language-reference
f1_keywords:
- dm_exec_query_optimizer_memory_gateways_TSQL
- dm_exec_query_optimizer_memory_gateways
- sys.dm_exec_query_optimizer_memory_gateways_TSQL
- sys.dm_exec_query_optimizer_memory_gateways
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_optimizer_memory_gateways dynamic management view
author: josack
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6e5c54d116f4d4d8a71ba3660a31b324d9952970
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405543"
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>Sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Devuelve el estado actual de semáforos de recursos que se utiliza para acelerar la optimización de consultas simultáneas.

|columna|Tipo|Descripción|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|Id. de grupo de recursos en el regulador de recursos|  
|**Nombre**|**sysname**|Compilar nombre gate (puerta de enlace pequeña, mediana de puerta de enlace, la puerta de enlace grande)|
|**número máximo**|**int**|El recuento máximo configurado de compilaciones simultáneas|
|**active_count**|**int**|El recuento de compilaciones en esta puerta activo actualmente|
|**waiter_count**|**int**|El número de tareas en espera en esta puerta|
|**threshold_factor**|**bigint**|Factor de umbral que define la parte de la memoria máxima utilizada por optimización de consultas.  Para la puerta de enlace pequeña threshold_factor indica el uso de memoria del optimizador máximo en bytes para una consulta antes de que sea necesario para obtener un acceso de la puerta de enlace pequeña.  Para la puerta de enlace mediana y grande, threshold_factor muestra la parte de la memoria total del servidor disponible para esta puerta. Se utiliza como un divisor al calcular el umbral de uso de memoria para la puerta.|
|**umbral**|**bigint**|Memoria de umbral siguiente en bytes.  La consulta es necesaria para obtener un acceso a esta puerta de enlace si su consumo de memoria alcanza este umbral.  "-1" si la consulta no es necesario para obtener un acceso a esta puerta de enlace.|
|**is_active**|**bit**|Si la consulta es necesario que pase la actual puerta o no.|


## <a name="permissions"></a>Permisos  
SQL Server requiere el permiso VIEW SERVER STATE en el servidor.

Azure SQL Database requiere el permiso VIEW DATABASE STATE en la base de datos.


## <a name="remarks"></a>Comentarios  
SQL Server usa un enfoque por niveles de la puerta de enlace para limitar al número de compilaciones simultáneas permitidas.  Se usan tres puertas de enlace, como pequeño, mediano y grande. Puertas de enlace de ayudar a evitar agotar los recursos de memoria general mayores consumidores de necesidad de memoria de compilación.

Se espera en un resultado de la puerta de enlace en la compilación diferida. Además de retrasos en la compilación, solicitudes limitadas tendrá un asociado RESOURCE_SEMAPHORE_QUERY_COMPILE acumulación del tipo de espera. El tipo de espera RESOURCE_SEMAPHORE_QUERY_COMPILE puede indicar que las consultas usan una gran cantidad de memoria para la compilación y que la memoria se ha agotado o, o bien no hay suficiente memoria disponible en general, las unidades disponibles pero en un determinado puerta de enlace se han agotado. La salida de **sys.dm_exec_query_optimizer_memory_gateways** puede usarse para solucionar problemas de escenarios donde había memoria suficiente para compilar un plan de ejecución de consulta.  

## <a name="examples"></a>Ejemplos  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. Visualizar las estadísticas de semáforos de recursos  
¿Cuáles son las estadísticas de puerta de enlace de memoria de optimizador actual para esta instancia de SQL Server?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con ejecuciones &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Cómo usar el comando DBCC MEMORYSTATUS para supervisar el uso de memoria en SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[espera de compilación de consulta de gran tamaño en RESOURCE_SEMAPHORE_QUERY_COMPILE en SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
