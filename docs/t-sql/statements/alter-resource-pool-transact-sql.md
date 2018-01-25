---
title: ALTER RESOURCE POOL (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_RESOURCE_POOL_TSQL
- ALTER RESOURCE POOL
dev_langs: TSQL
helpviewer_keywords: ALTER RESOURCE POOL
ms.assetid: 9c1c4cfb-0e3b-4f01-bf57-3fce94c7d1d4
caps.latest.revision: "47"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4edf3d8f20cc3705a6303d55f471dfa74c250f74
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="alter-resource-pool-transact-sql"></a>ALTER RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración del grupo de recursos de servidor del regulador de recursos existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER RESOURCE POOL { pool_name | "default" }  
[WITH  
    ( [ MIN_CPU_PERCENT = value ]  
    [ [ , ] MAX_CPU_PERCENT = value ]   
    [ [ , ] CAP_CPU_PERCENT = value ]   
    [ [ , ] AFFINITY {
                        SCHEDULER = AUTO 
                      | ( <scheduler_range_spec> ) 
                      | NUMANODE = ( <NUMA_node_range_spec> )
                      }]   
    [ [ , ] MIN_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_MEMORY_PERCENT = value ]   
    [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
    [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
)]   
[;]  
  
<scheduler_range_spec> ::=  
{SCHED_ID | SCHED_ID TO SCHED_ID}[,…n]  
  
<NUMA_node_range_spec> ::=  
{NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID}[,…n]  
```  
  
## <a name="arguments"></a>Argumentos  
 { *pool_name* | **"default"** }  
 Es el nombre de un grupo de recursos de servidor definido por el usuario ya existente o el grupo de recursos de servidor predeterminado creado al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 "default" debe estar encerrado entre comillas ("") o corchetes ([]) si se utiliza con ALTER RESOURCE POOL para evitar el conflicto con DEFAULT, que es una palabra reservada del sistema. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
> [!NOTE]  
>  Grupos de recursos y grupos de cargas de trabajo predefinido utilizan nombres en minúsculas, por ejemplo, "default". Debe tenerse esto en cuenta en los servidores que usan una intercalación que distingue entre mayúsculas y minúsculas. En los servidores que usan una intercalación que no distingue entre mayúsculas y minúsculas, como SQL_Latin1_General_CP1_CI_AS, los nombres "predeterminado" y "Predeterminado" son equivalentes.  
  
 MIN_CPU_PERCENT =*value*  
 Especifica el ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. *valor* es un entero con un valor predeterminado de 0. El intervalo permitido para *valor* está comprendido entre 0 y 100.  
  
 MAX_CPU_PERCENT =*value*  
 Especifica el promedio máximo de ancho banda de CPU que recibirán todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.  
  
 CAP_CPU_PERCENT =*value*  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica la capacidad máxima de CPU de destino para las solicitudes del grupo de recursos. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.  
  
> [!NOTE]  
>  Debido a la naturaleza estadística de la regulación de la CPU, puede que observe picos ocasionales si se supera el valor especificado en CAP_CPU_PERCENT.  
  
 AFFINITY {SCHEDULER = AUTO | (Scheduler_range_spec) | NUMANODE = (NUMA_node_range_spec)}  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Adjunte el grupo de recursos de servidor a los programadores específicos. El valor predeterminado es AUTO.  
  
 AFFINITY SCHEDULER = (Scheduler_range_spec) asigna al grupo de recursos a las programaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] representadas por los identificadores proporcionados. Estos identificadores se asignan a los valores de la columna scheduler_id de [sys.dm_os_schedulers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md).  
  
 Cuando usa AFFINITY NAMANODE = (NUMA_node_range_spec), se establece afinidad entre el grupo de recursos y a los programadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se asignan a las CPU físicas correspondientes al nodo NUMA o al intervalo de nodos especificado. Puede usar la siguiente consulta de Transact-SQL para detectar la asignación entre la configuración física de NUMA y los identificadores de programador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc 
   ON osn.node_id = sc.parent_node_id 
      AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*value*  
 Especifica la cantidad mínima de memoria reservada para este grupo de recursos de servidor que no se puede compartir con otros grupos de recursos de servidor. *valor* es un entero con un valor predeterminado de 0. El intervalo permitido para *valor* está comprendido entre 0 y 100.  
  
 MAX_MEMORY_PERCENT =*value*  
 Especifica la memoria total del servidor que puede ser utilizada por las solicitudes en este grupo de recursos de servidor. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.  
  
 MIN_IOPS_PER_VOLUME =*valor*  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el número mínimo de operaciones de E/S por segundo (IOPS) por volumen de disco que se deben reservar para el grupo de recursos de servidor. El intervalo permitido para *valor* está comprendido entre 0 y 2 ^ 31-1 (2.147.483.647). Especifique 0 si no desea indicar un umbral mínimo para el grupo.  
  
 MAX_IOPS_PER_VOLUME =*valor*  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el número máximo de operaciones de E/S por segundo (IOPS) por volumen de disco que se deben permitir para el grupo de recursos de servidor. El intervalo permitido para *valor* está comprendido entre 0 y 2 ^ 31-1 (2.147.483.647). Especifique 0 para establecer un umbral ilimitado para el grupo. El valor predeterminado es 0.  
  
 Si MAX_IOPS_PER_VOLUME se establece en 0 para un grupo, este no está regulado y puede tomar todas las IOPS del sistema, incluso aunque otros grupos tengan establecido un valor MIN_IOPS_PER_VOLUME. En este caso, se recomienda establecer el valor de MAX_IOPS_PER_VOLUME para este grupo en un número alto (por ejemplo, el valor máximo 2^31-1) si desea que se regule la E/S de este grupo.  
  
## <a name="remarks"></a>Comentarios  
 MAX_CPU_PERCENT y MAX_MEMORY_PERCENT deben ser mayores o iguales que MIN_CPU_PERCENT y MIN_MEMORY_PERCENT, respectivamente.  
  
 MAX_CPU_PERCENT puede utilizar la capacidad de CPU por encima del valor de MAX_CPU_PERCENT si está disponible. Aunque puede haber periódicos picos anteriormente CAP_CPU_PERCENT, las cargas de trabajo no puede exceder CAP_CPU_PERCENT durante largos períodos de tiempo, incluso cuando la capacidad de CPU adicional está disponible.  
  
 El porcentaje total de la CPU para cada componente afín (programadores o nodos NUMA) no debe superar el 100 %.  
  
 Si va a ejecutar instrucciones de DDL, se recomienda familiarizarse primero con los estados del regulador de recursos. Para obtener más información, consulte [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md).  
  
 Cuando se cambia un plan que afectan a la configuración, la nueva configuración sólo se aplicará en los planes previamente almacenado en caché después de ejecutar DBCC FREEPROCCACHE (*pool_name*), donde *pool_name* es el nombre de un recurso Regulador de recursos.  
  
-   Si va a cambiar la AFINIDAD de varios programadores a un programador único, la ejecución de DBCC FREEPROCCACHE no es necesario porque planes paralelos pueden ejecutarse en modo de serie. Sin embargo, no puede ser tan eficaz como un plan compilado como un plan en serie.  
  
-   Si va a cambiar la AFINIDAD de un solo programador a los programadores varios, no es necesario ejecutar DBCC FREEPROCCACHE. Sin embargo, los planes en serie no se puede ejecutar en paralelo, para borrar la memoria caché respectiva le permitirá potencialmente nuevos planes para compilarse con paralelismo.  
  
> [!CAUTION]  
>  Borrar los planes almacenados en caché de un grupo de recursos que está asociado a más de un grupo de cargas de trabajo afectará a todos los grupos de cargas de trabajo con el grupo de recursos definidos por el usuario identificado por *pool_name*.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente mantiene toda la configuración predeterminada del grupo de recursos de servidor en el grupo `default`, salvo `MAX_CPU_PERCENT`, que se cambia a `25`.  
  
```  
ALTER RESOURCE POOL "default"  
WITH  
     ( MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 En el ejemplo siguiente, `CAP_CPU_PERCENT` establece el límite máximo en 80 % y `AFFINITY SCHEDULER` se establece según un valor individual de 8 y un intervalo de 12 a 16.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER RESOURCE POOL Pool25  
WITH(   
     MIN_CPU_PERCENT = 5,  
     MAX_CPU_PERCENT = 10,       
     CAP_CPU_PERCENT = 80,  
     AFFINITY SCHEDULER = (8, 12 TO 16),   
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
);  
  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
