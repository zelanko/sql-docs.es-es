---
title: CREATE EXTERNAL RESOURCE POOL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL RESOURCE POOL
- CREATE EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE POOL
- EXTERNAL_RESOURCE_POOL_TSQL
- EXTERNAL RESOURCE
- EXTERNAL_RESOURCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL RESOURCE POOL statement
ms.assetid: 8cc798ad-c395-461c-b7ff-8c561c098808
author: dphansen
ms.author: davidph
manager: cgronlund
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: dc83d3f63478001fccaabfd9fa431652434b0c6c
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471176"
---
# <a name="create-external-resource-pool-transact-sql"></a>CREATE EXTERNAL RESOURCE POOL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

Crea un grupo externo que sirve para definir los recursos de los procesos externos. Un grupo de recursos de servidor representa un subconjunto de los recursos físicos (memoria y CPU) de una instancia del motor de base de datos. El Regulador de recursos permite que un administrador de bases de datos distribuya los recursos del servidor entre los grupos de recursos, hasta un máximo de 64 grupos.

+ En [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], el grupo externo rige `rterm.exe`, `BxlServer.exe` y otros procesos generados por ellos.

+ En [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] en [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], el grupo externo rige `rterm.exe`, `python.exe`, `BxlServer.exe` y otros procesos generados por ellos.

  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
CREATE EXTERNAL RESOURCE POOL pool_name  
[ WITH (  
    [ MAX_CPU_PERCENT = value ]  
    [ [ , ] AFFINITY CPU =    
            {  
                AUTO   
              | ( <cpu_range_spec> )   
              | NUMANODE = ( <NUMA_node_id> )   
            } ]   
    [ [ , ] MAX_MEMORY_PERCENT = value ]  
    [ [ , ] MAX_PROCESSES = value ]   
    )   
]  
[ ; ]  
  
<CPU_range_spec> ::=    
{ CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]  
```  
  
## <a name="arguments"></a>Argumentos

*pool_name*  
Es el nombre definido por el usuario para identificar el grupo de recursos externos. *pool_name* es alfanumérico y puede tener hasta 128 caracteres. Este argumento debe ser únicos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cumplir las reglas de los [identificadores](../../relational-databases/databases/database-identifiers.md).  

MAX_CPU_PERCENT =*value*  
Especifica el promedio máximo de ancho de banda de CPU que pueden recibir todas las solicitudes en el grupo de recursos externo cuando haya contención de CPU. *value* es un entero con un valor predeterminado de 100. El intervalo permitido para *value* es de 1 a 100.

AFFINITY {CPU = AUTO | ( \<CPU_range_spec> ) | NUMANODE = (\<NUMA_node_range_spec>)} Adjunte el grupo de recursos externos a CPU concretas. El valor predeterminado es AUTO.

AFFINITY CPU = **(** \<CPU_range_spec> **)** asigna el grupo de recursos externos a las CPU de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificadas por los CPU_ID dados.

Cuando se usa AFFINITY NUMANODE = **(** \<NUMA_node_range_spec> **)** , se establece una afinidad entre el grupo de recursos externos y las CPU físicas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondientes al nodo o al intervalo de nodos NUMA especificado. 

MAX_MEMORY_PERCENT =*value*  
Especifica la memoria total del servidor que puede ser usada por las solicitudes en este grupo de recursos externos. *value* es un entero con un valor predeterminado de 100. El intervalo permitido para *value* es de 1 a 100.

MAX_PROCESSES =*value*  
Especifica el número máximo de procesos permitidos para el grupo de recursos externos. Especifique 0 para establecer un umbral ilimitado para el grupo, que estará enlazado solamente por recursos del equipo. El valor predeterminado es 0.

## <a name="remarks"></a>Notas

El [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa el grupo de recursos al ejecutar la instrucción [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md).

Para obtener información general sobre los grupos de recursos, vea [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md) y [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).

Para obtener información específica sobre cómo administrar los grupos de recursos externos usados en el aprendizaje automático, vea [Resource governance for machine learning in SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md) (Gobernanza de recursos para aprendizaje automático en SQL Server). 

## <a name="permissions"></a>Permisos

Requiere el permiso `CONTROL SERVER`.

## <a name="examples"></a>Ejemplos

La siguiente instrucción define un grupo externo que restringe el uso de CPU al 75 por ciento. La instrucción también define la cantidad máxima de memoria al 30 por ciento de la memoria disponible en el equipo.

```sql
CREATE EXTERNAL RESOURCE POOL ep_1
WITH (  
    MAX_CPU_PERCENT = 75
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 30
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```
  
## <a name="see-also"></a>Vea también

[Opción de configuración del servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)
[sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)
[ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)
[DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)
[CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
[CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)
[Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md)
[sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)
[sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)
[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)
