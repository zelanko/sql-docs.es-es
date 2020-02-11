---
title: Sys. dm_os_job_object (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 43063bb56607d1b5a21ae04b40ee4c7a17825521
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67900136"
---
# <a name="sysdm_os_job_object-azure-sql-database"></a>sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Devuelve una sola fila que describe la configuración del objeto de trabajo que administra el proceso de SQL Server, así como ciertas estadísticas de consumo de recursos en el nivel de objeto de trabajo. Devuelve un conjunto vacío si SQL Server no se está ejecutando en un objeto de trabajo. 

Un objeto de trabajo es una construcción de Windows que implementa la CPU, la memoria y el gobierno de recursos de e/s en el nivel del sistema operativo. Para obtener más información sobre los objetos de trabajo, vea [objetos de trabajo](/windows/desktop/ProcThread/job-objects). 
  
|Columnas|Tipo de datos|Descripción|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Especifica la parte de los ciclos del procesador que los subprocesos de SQL Server pueden utilizar durante cada intervalo de programación. El valor se muestra como un porcentaje de los ciclos disponibles dentro de un intervalo de programación del ciclo 10000. Por ejemplo, el valor 100 significa que los subprocesos pueden usar los núcleos de CPU tienen toda su capacidad.|
|cpu_affinity_mask|**BIGINT**|Máscara de bits que describe qué procesadores lógicos puede utilizar el SQL Server proceso en el grupo de procesadores. Por ejemplo, cpu_affinity_mask 255 (1111 1111 en binario) significa que se pueden usar los primeros ocho procesadores lógicos.|
|cpu_affinity_group|**int**|El número del grupo de procesadores que usa SQL Server.|
|memory_limit_mb|**BIGINT**|Cantidad máxima de memoria asignada, en MB, que todos los procesos del objeto de trabajo, incluido SQL Server, pueden usar de manera acumulativa.| 
|process_memory_limit_mb |**BIGINT**|La cantidad máxima de memoria asignada, en MB, que un único proceso en el objeto de trabajo, como SQL Server, puede usar.|
|workingset_limit_mb |**BIGINT**|Cantidad máxima de memoria, en MB, que puede usar el espacio de trabajo de SQL Server.|
|non_sos_mem_gap_mb|**BIGINT**|Cantidad de memoria, en MB, reservada para pilas de subprocesos, archivos dll y otras asignaciones de memoria no SOS. La memoria de destino de SOS es `process_memory_limit_mb` la `non_sos_mem_gap_mb`diferencia entre y.| 
|low_mem_signal_threshold_mb|**BIGINT**|Umbral de memoria, en MB. Cuando la cantidad de memoria disponible para el objeto de trabajo está por debajo de este umbral, se envía una señal de notificación de memoria baja al proceso de SQL Server. |
|total_user_time|**BIGINT**|El número total de 100 pasos NS que los subprocesos del objeto de trabajo han pasado en modo de usuario, desde que se creó el objeto de trabajo. |
|total_kernel_time |**BIGINT**|El número total de 100 pasos NS que los subprocesos del objeto de trabajo han pasado en modo kernel, desde que se creó el objeto de trabajo. |
|write_operation_count |**BIGINT**|El número total de operaciones de e/s de escritura en los discos locales emitidos por SQL Server desde que se creó el objeto de trabajo. |
|read_operation_count |**BIGINT**|El número total de operaciones de e/s de lectura en discos locales emitidos por SQL Server desde que se creó el objeto de trabajo. |
|peak_process_memory_used_mb|**BIGINT**|Cantidad máxima de memoria, en MB, que un único proceso en el objeto de trabajo, como SQL Server, ha usado desde que se creó el objeto de trabajo.| 
|peak_job_memory_used_mb|**BIGINT**|Cantidad máxima de memoria, en MB, que todos los procesos del objeto de trabajo han utilizado de manera acumulativa desde que se creó el objeto de trabajo.|
  
## <a name="permissions"></a>Permisos  
En Instancia administrada de SQL Database, requiere `VIEW SERVER STATE` el permiso. En SQL Database, se requiere el permiso `VIEW DATABASE STATE` en la base de datos.  
 
## <a name="see-also"></a>Consulte también  

Para obtener información acerca de las instancias administradas, consulte [instancia administrada de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
