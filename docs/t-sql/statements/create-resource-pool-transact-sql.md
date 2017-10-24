---
title: Crear grupo de recursos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE RESOURCE POOL
- RESOURCE POOL
- CREATE_RESOURCE_POOL_TSQL
- RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE RESOURCE POOL
ms.assetid: 82712505-c6f9-4a65-a469-f029b5a2d6cd
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c6f9a6ae8f0f869eb5ddd32c0189fcbaab198d3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-resource-pool-transact-sql"></a>CREATE RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un grupo de recursos de servidor del regulador de recursos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un grupo de recursos de servidor representa un subconjunto de los recursos físicos (memoria, CPU y E/S) de una instancia del motor de base de datos. El Regulador de recursos permite que un administrador de bases de datos distribuya los recursos del servidor entre los grupos de recursos, hasta un máximo de 64 grupos. El regulador de recursos no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE RESOURCE POOL pool_name  
[ WITH  
    (  
        [ MIN_CPU_PERCENT = value ]  
        [ [ , ] MAX_CPU_PERCENT = value ]   
        [ [ , ] CAP_CPU_PERCENT = value ]   
        [ [ , ] AFFINITY {SCHEDULER =  
                  AUTO 
                | ( <scheduler_range_spec> )   
                | NUMANODE = ( <NUMA_node_range_spec> )
                } ]   
        [ [ , ] MIN_MEMORY_PERCENT = value ]  
        [ [ , ] MAX_MEMORY_PERCENT = value ]  
        [ [ , ] MIN_IOPS_PER_VOLUME = value ]  
        [ [ , ] MAX_IOPS_PER_VOLUME = value ]  
    )   
]  
[;]  
  
<scheduler_range_spec> ::=  
{ SCHED_ID | SCHED_ID TO SCHED_ID }[,…n]  
  
<NUMA_node_range_spec> ::=  
{ NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID }[,…n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *pool_name*  
 Es el nombre definido por el usuario para identificar el grupo de recursos de servidor. *pool_name* es alfanumérico, puede tener hasta 128 caracteres, deben ser únicos dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 MIN_CPU_PERCENT =*valor*  
 Especifica el ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. *valor* es un entero con un valor predeterminado de 0. El intervalo permitido para *valor* está comprendido entre 0 y 100.  
  
 MAX_CPU_PERCENT =*valor*  
 Especifica el ancho de banda de CPU promedio máximo que recibirán todas las solicitudes del grupo de recursos de servidor cuando hay contención de CPU. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.  
  
 CAP_CPU_PERCENT =*valor*  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica un límite máximo de ancho de banda de CPU que recibirán todas las solicitudes del grupo de recursos de servidor. Limita el nivel de ancho de banda máximo de CPU para que coincida con el valor especificado. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.  
  
 AFINIDAD {PROGRAMADOR = AUTO | ( \<scheduler_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)} **se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Adjunte el grupo de recursos de servidor a los programadores específicos. El valor predeterminado es AUTO.  
  
 AFFINITY SCHEDULER = **(** \<scheduler_range_spec > **)** asigna el grupo de recursos para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programaciones identificadas por los identificadores especificados. Estos identificadores se asignan a los valores de la columna scheduler_id de [sys.dm_os_schedulers &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 
  
 Cuando usa AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**, se establece la afinidad del grupo de recursos para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programadores que se asignan a las CPU físicas correspondientes a el nodo NUMA o al intervalo de nodos. Puede usar la siguiente consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] para detectar la asignación entre la configuración física de NUMA y los identificadores de programador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
  
```  
SELECT osn.memory_node_id AS [numa_node_id], sc.cpu_id, sc.scheduler_id  
FROM sys.dm_os_nodes AS osn  
INNER JOIN sys.dm_os_schedulers AS sc   
    ON osn.node_id = sc.parent_node_id   
    AND sc.scheduler_id < 1048576;  
```  
  
 MIN_MEMORY_PERCENT =*valor*  
 Especifica la cantidad mínima de memoria reservada para este grupo de recursos de servidor que no se puede compartir con otros grupos de recursos de servidor. *valor* es un entero con un valor predeterminado de 0 del intervalo permitido para *valor* está comprendido entre 0 y 100.  
  
 MAX_MEMORY_PERCENT =*valor*  
 Especifica la memoria total del servidor que puede ser utilizada por las solicitudes en este grupo de recursos de servidor. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.  
  
 MIN_IOPS_PER_VOLUME =*valor*  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el número mínimo de operaciones de E/S por segundo (IOPS) por volumen de disco que se deben reservar para el grupo de recursos de servidor. El intervalo permitido para *valor* está comprendido entre 0 y 2 ^ 31-1 (2.147.483.647). Especifique 0 si no desea indicar un umbral mínimo para el grupo. El valor predeterminado es 0.  
  
 MAX_IOPS_PER_VOLUME =*valor*  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica el número máximo de operaciones de E/S por segundo (IOPS) por volumen de disco que se deben permitir para el grupo de recursos de servidor. El intervalo permitido para *valor* está comprendido entre 0 y 2 ^ 31-1 (2.147.483.647). Especifique 0 para establecer un umbral ilimitado para el grupo. El valor predeterminado es 0.  
  
 Si MAX_IOPS_PER_VOLUME se establece en 0 para un grupo, este no está regulado y puede tomar todas las IOPS del sistema, incluso aunque otros grupos tengan establecido un valor MIN_IOPS_PER_VOLUME. En este caso, se recomienda establecer el valor de MAX_IOPS_PER_VOLUME para este grupo en un número alto (por ejemplo, el valor máximo 2^31-1) si desea que se regule la E/S de este grupo.  
  
## <a name="remarks"></a>Comentarios  
 MIN_IOPS_PER_VOLUME y MAX_IOPS_PER_VOLUME especifican las lecturas o escrituras mínimas y máximas por segundo. Estas lecturas o escrituras pueden ser de cualquier tamaño y no indican un rendimiento mínimo o máximo.  
  
 Los valores de MAX_CPU_PERCENT y MAX_MEMORY_PERCENT deben ser mayores o iguales que los valores de MIN_CPU_PERCENT y MIN_MEMORY_PERCENT, respectivamente.  
  
 CAP_CPU_PERCENT se diferencia de MAX_CPU_PERCENT en que las cargas de trabajo asociadas al grupo pueden utilizar capacidad de CPU por encima del valor de MAX_CPU_PERCENT, si se encuentra disponible, pero no por encima del valor de CAP_CPU_PERCENT.  
  
 El porcentaje total de la CPU para cada componente afín (programadores o nodos NUMA) no debe superar el 100 %.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo crear un grupo de recursos denominado `bigPool`. Este grupo utiliza los valores predeterminados del regulador de recursos.  
  
```  
CREATE RESOURCE POOL bigPool;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 En el ejemplo siguiente se establece el valor de `CAP_CPU_PERCENT` en un límite máximo de 30 % y `AFFINITY SCHEDULER` en un intervalo de 0 a 63, 128 a 191. 
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
     MIN_CPU_PERCENT = 10,  
     MAX_CPU_PERCENT = 20,  
     CAP_CPU_PERCENT = 30,  
     AFFINITY SCHEDULER = (0 TO 63, 128 TO 191),  
     MIN_MEMORY_PERCENT = 5,  
     MAX_MEMORY_PERCENT = 15  
      );  
  
```  
  
 El siguiente ejemplo se establece `MIN_IOPS_PER_VOLUME` a \<algún valor > y `MAX_IOPS_PER_VOLUME` a \<algún valor >. Estos valores controlan las operaciones de lectura y escritura de E/S física disponibles para el grupo de recursos de servidor.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE RESOURCE POOL PoolAdmin  
WITH (  
    MIN_IOPS_PER_VOLUME = 20,  
    MAX_IOPS_PER_VOLUME = 100  
      );  
  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Crear un grupo de recursos de servidor](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
  


