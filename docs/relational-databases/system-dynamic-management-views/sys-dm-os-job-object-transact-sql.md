---
title: Sys.dm_os_job_object (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8ab408179388ca10821ad79e855e39fd3ec7eb01
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37968767"
---
# <a name="sysdmosjobobject-azure-sql-database"></a>Sys.dm_os_job_object (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

Devuelve una sola fila que describe la configuración del objeto de trabajo que administra el proceso de SQL Server, así como ciertas estadísticas de consumo de recursos en el nivel de objeto de trabajo. Devuelve un conjunto vacío si no se está ejecutando SQL Server en un objeto de trabajo. 

Un objeto de trabajo es una construcción de Windows que implementa la regulación de recursos de CPU, memoria y E/S en el nivel de sistema operativo. Para obtener más información acerca de los objetos de trabajo, consulte [objetos de trabajo](https://msdn.microsoft.com/library/windows/desktop/ms684161.aspx). 

> [!NOTE]
> El sys.dm_os_job_object DMV actualmente puede aparecer como sys.dm_job_object. Esto es temporal: `sys.dm_os_job_object` será el nombre de esta DMV permanente. 
  
|Columnas|Tipo de datos|Descripción|  
|-------------|---------------|-----------------|  
|cpu_rate|**int**|Especifica la parte de los ciclos de procesador que pueden usar los subprocesos de SQL Server durante cada intervalo de programación. El valor se notifica como un porcentaje de ciclos disponibles dentro de un intervalo de programación de ciclo de 10000. Por ejemplo, el valor 100 significa que subprocesos pueden usar núcleos de CPU es su máxima capacidad.|
|cpu_affinity_mask|**bigint**|Una máscara de bits que describe qué procesadores lógicos del proceso de SQL Server puede usar en el grupo de procesadores. Por ejemplo, cpu_affinity_mask 255 (1111 1111 en formato binario) significa que los ocho primeros se pueden usar procesadores lógicos.|
|cpu_affinity_group|**int**|El número del grupo de procesadores que se usa SQL Server.|
|memory_limit_mb|**bigint**|La cantidad máxima de memoria confirmada, en MB, que todos los procesos en el objeto de trabajo, incluido SQL Server, pueden usar de manera acumulativa.| 
|process_memory_limit_mb |**bigint**|La cantidad máxima de memoria confirmada, en MB, que un solo proceso en el objeto de trabajo, como SQL Server, puede usar.|
|workingset_limit_mb |**bigint**|La cantidad máxima de memoria, en MB, que puede usar el espacio de trabajo de SQL Server.|
|non_sos_mem_gap_mb|**bigint**|La cantidad de memoria en MB, se reservan para las pilas de subprocesos, los archivos DLL y otras asignaciones de memoria que no sean de SOS. Memoria de destino de SOS es la diferencia entre `process_memory_limit_mb` y `non_sos_mem_gap_mb`.| 
|low_mem_signal_threshold_mb|**bigint**|Umbral de memoria, en MB. Cuando la cantidad de memoria disponible para el objeto de trabajo está por debajo del umbral, se envía una señal de notificación de memoria insuficiente para el proceso de SQL Server. |
|total_user_time|**bigint**|El número total de tics de 100 ns que los subprocesos dentro del objeto de trabajo ha empleado en modo de usuario, desde que se creó el objeto de trabajo. |
|total_kernel_time |**bigint**|El número total de tics de 100 ns que los subprocesos dentro del objeto de trabajo ha empleado en modo de núcleo, desde que se creó el objeto de trabajo. |
|write_operation_count |**bigint**|El número total de operaciones de E/S de discos locales emitidas por SQL Server desde que se creó el objeto de trabajo de escritura. |
|read_operation_count |**bigint**|El número total de operaciones de E/S de lectura de discos locales emitidas por SQL Server desde que se creó el objeto de trabajo. |
|peak_process_memory_used_mb|**bigint**|La cantidad máxima de memoria, en MB, que un único proceso en el objeto de trabajo, como SQL Server, se ha usado desde que se creó el objeto de trabajo.| 
|peak_job_memory_used_mb|**bigint**|La cantidad máxima de memoria, en MB, que todos los procesos en el objeto de trabajo han utilizado de manera acumulativa puesto que el objeto de trabajo se creó.|
  
## <a name="permissions"></a>Permisos  
Base de datos de instancia administrada de SQL, requiere `VIEW SERVER STATE` permiso. En la base de datos de SQL, requiere el `VIEW DATABASE STATE` permiso en la base de datos.  
 
## <a name="see-also"></a>Vea también  

Para obtener información sobre instancias administradas, vea [instancia administrada de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).
  
