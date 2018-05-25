---
title: Sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL) | Documentos de Microsoft
description: Devuelve el estado actual de semáforos de recursos que se utiliza para acelerar la optimización de consultas simultáneas
ms.custom: ''
ms.date: 04/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b9d36c4a67fab2f9f7c867a3ba6b7e7d01fc5d29
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmexecqueryoptimizermemorygateways-transact-sql"></a>Sys.dm_exec_query_optimizer_memory_gateways (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Devuelve el estado actual de semáforos de recursos que se utiliza para acelerar la optimización de consultas simultáneas.

|Columna|Tipo|Description|  
|----------|---------------|-----------------|  
|**pool_id**|**int**|Id. de grupo de recursos en el regulador de recursos|  
|**Nombre**|**sysname**|Compile el nombre de la puerta (pequeña puerta de enlace, mediano, grande puerta de enlace)|
|**número máximo**|**int**|El recuento máximo configurado de compilaciones simultáneas|
|**active_count**|**int**|El número activo actualmente de compilaciones en esta puerta|
|**waiter_count**|**int**|El número de esperas en esta puerta|
|**threshold_factor**|**bigint**|Factor de umbral que define la parte de memoria máxima utilizada por la optimización de consultas.  La puerta de enlace pequeño, threshold_factor indica el uso de memoria del optimizador máximo en bytes para una consulta antes de que sea necesario para obtener un acceso en la puerta de enlace pequeño.  La puerta de enlace de mediano y grande, threshold_factor muestra la parte de la memoria total del servidor disponible para esta puerta. Se utiliza como un divisor al calcular el umbral de uso de memoria para la puerta.|
|**Umbral**|**bigint**|Memoria de umbral siguiente en bytes.  La consulta debe tener un acceso a esta puerta de enlace si su consumo de memoria alcanza este límite.  "-1" si la consulta no es necesaria para obtener un acceso a esta puerta de enlace.|
|**is_active**|**bit**|Si la consulta tiene que pasar la puerta actual o no.|


## <a name="permissions"></a>Permissions  
SQL Server requiere el permiso VIEW SERVER STATE en el servidor.

La base de datos de SQL Azure requiere el permiso VIEW DATABASE STATE en la base de datos.


## <a name="remarks"></a>Comentarios  
SQL Server usa un enfoque en capas de la puerta de enlace para limitar al número de compilaciones simultáneas permitidas.  Se usan tres puertas de enlace, incluidas las pequeñas, medianas y grandes. Las puertas de enlace ayudan a evitar el agotamiento de recursos totales de memoria por los consumidores de necesidad de memoria de compilación más grandes.

Espera a que en un resultado de la puerta de enlace en la compilación diferida. Además de retrasos en la compilación, las solicitudes limitadas tendrá una RESOURCE_SEMAPHORE_QUERY_COMPILE asociado acumulación de tipo de espera. El tipo de espera RESOURCE_SEMAPHORE_QUERY_COMPILE puede indicar que las consultas utilizan una gran cantidad de memoria de compilación y que la memoria se ha agotado o, o bien no hay suficiente memoria disponible en general, las unidades sin embargo disponibles en un determinado puerta de enlace se han agotado. La salida de **sys.dm_exec_query_optimizer_memory_gateways** puede usarse para solucionar problemas de escenarios donde había memoria suficiente para compilar un plan de ejecución de consulta.  

## <a name="examples"></a>Ejemplos  

### <a name="a-viewing-statistics-on-resource-semaphores"></a>A. Visualizar las estadísticas de semáforos de recursos  
¿Cuáles son las estadísticas de puerta de enlace de memoria optimizador actual para esta instancia de SQL Server?

```  
SELECT [pool_id], [name], [max_count], [active_count],
       [waiter_count], [threshold_factor], [threshold],
       [is_active]
FROM sys.dm_exec_query_optimizer_memory_gateways;   

```  

## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](./system-dynamic-management-views.md)   
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](./execution-related-dynamic-management-views-and-functions-transact-sql.md)  
[Cómo usar el comando DBCC MEMORYSTATUS para supervisar el uso de memoria en SQL Server 2005](https://support.microsoft.com/help/907877/how-to-use-the-dbcc-memorystatus-command-to-monitor-memory-usage-on-sql-server-2005)
[compilación de consulta de gran tamaño, se espera en RESOURCE_SEMAPHORE_QUERY_COMPILE en SQL Server 2014](https://support.microsoft.com/help/3024815/large-query-compilation-waits-on-resource-semaphore-query-compile-in-sql-server-2014)
