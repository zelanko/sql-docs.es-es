---
title: Modificar grupo de recursos externo (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_EXTERNAL_RESOURCE_POOL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL RESOURCE POOL statement
ms.assetid: 634c327d-971b-49ba-b8a2-e243a04040db
caps.latest.revision: 
author: jeannt
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb4073a8114e953dc9df87614a63e074ab8c9683
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="alter-external-resource-pool-transact-sql"></a>Modificar grupo de recursos externo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] y [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

Modifica un grupo externo de regulador de recursos que especifica los recursos que pueden usarse en procesos externos. 

+ Para [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], el grupo externo rige `rterm.exe`, `BxlServer.exe`y otros procesos generados por ellos.

+ Para [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] en SQL Server 2017, el grupo externo rige los procesos de R aparece en la versión anterior, así como `python.exe`, `BxlServer.exe`y otros procesos generados por ellos.

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxis

```sql
ALTER EXTERNAL RESOURCE POOL { pool_name | "default" }
[ WITH (
    [ MAX_CPU_PERCENT = value ]
    [ [ , ] AFFINITY CPU =
            {
                AUTO
              | ( <cpu_range_spec> )
              | NUMANODE = (( <NUMA_node_id> )
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

{ *pool_name* | "default"}  
Es el nombre de un grupo existente de un recurso externo definido por el usuario o el grupo de recursos externo predeterminado que se crea cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.
"default" debe estar entre comillas ("") o corchetes ([]) cuando se usa con `ALTER EXTERNAL RESOURCE POOL` para evitar el conflicto con `DEFAULT`, que es un sistema palabra reservada.


MAX_CPU_PERCENT =*valor*  
Especifica el medio CPU ancho de banda máximo que pueden recibir todas las solicitudes del grupo de recursos externos cuando hay contención de CPU. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.


AFINIDAD {CPU = AUTO | ( \<CPU_range_spec >) | NUMANODE = (\<NUMA_node_range_spec >)}  
Conecte el grupo de recursos externos a una CPU específica. El valor predeterminado es AUTO.

AFINIDAD de CPU = **(** \<CPU_range_spec > **)** asigna el grupo de recursos externos a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU identificado por la CPU_IDs determinado. Cuando usa AFFINITY NUMANODE = **(** \<NUMA_node_range_spec > **)**, se establece la afinidad el grupo de recursos externos a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU físicas correspondientes a la determinada NUMA nodo o un rango de nodos.


MAX_MEMORY_PERCENT =*valor*  
Especifica la memoria total del servidor que puede utilizarse en las solicitudes en este grupo de recursos externos. *valor* es un entero con un valor predeterminado de 100. El intervalo permitido para *valor* está comprendido entre 1 y 100.


MAX_PROCESSES =*valor*  
Especifica el número máximo de procesos permitidos para el grupo de recursos externos. Especifique 0 para establecer un umbral ilimitado para el grupo, que está enlazado a partir de ahí por los recursos del equipo. El valor predeterminado es 0.

## <a name="remarks"></a>Comentarios

El [!INCLUDE[ssDE](../../includes/ssde-md.md)] implementa el grupo de recursos al ejecutar el [ALTER RESOURCE GOVERNOR RECONFIGURE](../../t-sql/statements/alter-resource-governor-transact-sql.md) instrucción.

Para obtener información general acerca de los grupos de recursos, consulte [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md), [sys.resource_governor_external_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), y [sys.dm_resource_governor_external_resource_pool_affinity &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md).  

Para obtener información específica para el uso de grupos de recursos externos para controlar trabajos de aprendizaje de máquina, vea [regulador de recursos para el aprendizaje automático en SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)...
## <a name="permissions"></a>Permissions

Requiere `CONTROL SERVER` permiso.

## <a name="examples"></a>Ejemplos

La instrucción siguiente cambia un grupo externo, restringir el uso de CPU a 50 por ciento y la memoria máxima al 25 por ciento de la memoria disponible en el equipo.
  
```sql
ALTER EXTERNAL RESOURCE POOL ep_1
WITH (
    MAX_CPU_PERCENT = 50
    , AFFINITY CPU = AUTO
    , MAX_MEMORY_PERCENT = 25
);
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>Vea también

[Regulación de recursos para el aprendizaje automático en SQL Server](../../advanced-analytics/r/resource-governance-for-r-services.md)

[Opción de configuración de servidor Scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)

[CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

[Eliminar grupo de recursos externo &#40; Transact-SQL &#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)

[ALTER RESOURCE POOL &#40; Transact-SQL &#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)

[Crear grupo de cargas de trabajo &#40; Transact-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md)

[Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

[ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md) 
