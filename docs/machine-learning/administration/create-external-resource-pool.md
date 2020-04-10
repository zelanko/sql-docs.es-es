---
title: Creación de un grupo de recursos
description: Obtenga información sobre cómo crear y usar un grupo de recursos para administrar cargas de trabajo de Python o R en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f8661101fa5b0f859723a168e149ae9747b3da4
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81119038"
---
# <a name="create-a-resource-pool-for-sql-server-machine-learning-services"></a>Crear un grupo de recursos para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Obtenga información sobre cómo crear y usar un grupo de recursos para administrar cargas de trabajo de Python o R en SQL Server Machine Learning Services. 

El proceso incluye varios pasos:

1. Estado de revisión de cualquiera de los grupos de recursos existente. Es importante que comprenda qué servicios están usando los recursos existentes.
2. Modificar grupos de recursos de servidor.
3. Crear un nuevo grupo de recursos para los procesos externos.
4. Cree una función de clasificación para identificar las solicitudes de script externas.
5. Compruebe que el nuevo grupo de recursos externos está capturando trabajos de Python o R de las cuentas o los clientes especificados.

<a name="bkmk_ReviewStatus"></a>

##  <a name="review-the-status-of-existing-resource-pools"></a>Estado de revisión de los grupos de recursos existentes
  
1.  Use una instrucción como la siguiente para comprobar los recursos asignados al grupo predeterminado para el servidor.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **Ejemplo de resultados**

    |{1}pool_id{2}|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|default|0|100|0|100|100|0|0|

2.  Compruebe los recursos asignados al grupo de recursos **externos** predeterminado.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **Ejemplo de resultados**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
 
3.  Con estos valores predeterminados de servidor, es probable que el tiempo de ejecución externo no tenga recursos suficientes para completar la mayoría de las tareas. Para cambiar esta configuración, se debe modificar el uso de recursos de servidor de la siguiente manera:
  
    -   Reducir la memoria máxima del equipo que puede usar el motor de base de datos.
  
    -   Aumentar la memoria máxima del equipo que puede usar el proceso externo.

## <a name="modify-server-resource-usage"></a>Modificar el uso de recursos de servidor

1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la siguiente instrucción para limitar el uso de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al **60 %** del valor de la opción "max server memory".

    ```sql
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);
    ```
  
2.  De forma similar, ejecute la instrucción siguiente para limitar el uso de memoria de los procesos externos al **40 %** de los recursos totales del equipo.
  
    ```sql
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);
    ```
  
3.  Para aplicar estos cambios, debe volver a configurar y reiniciar Resource Governor de esta forma:
  
    ```sql
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
    > [!NOTE]
    >  Estas son solo opciones iniciales sugeridas. Debe evaluar las tareas de aprendizaje automático en función de otros procesos del servidor para determinar el equilibrio correcto para el entorno y la carga de trabajo.

## <a name="create-a-user-defined-external-resource-pool"></a>Crear un grupo de recursos externos definido por el usuario
  
1.  Los cambios en la configuración de Resource Governor se aplican en todo el servidor como un todo y afectan a las cargas de trabajo que usan los grupos predeterminados para el servidor, así como a las cargas de trabajo que usan los grupos externos.
  
     Por tanto, para proporcionar un mayor control sobre qué cargas de trabajo deben tener prioridad, puede crear un nuevo grupo de recursos externos definido por el usuario. También debe definir una función de clasificación y asignarla al grupo de recursos externos. La palabra clave **EXTERNAL** es nueva.
  
     Empiece por crear un nuevo *grupo de recursos externos definido por el usuario*. En el ejemplo siguiente, el grupo se denomina **ds_ep**.
  
    ```sql
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);
    ```

2.  Cree un grupo de cargas de trabajo denominado `ds_wg` para usar en la administración de solicitudes de sesión. Para las consultas SQL, usará el grupo predeterminado. Para las consultas de procesos externos usará el grupo `ds_ep`.
  
    ```sql
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";
    ```
  
     Las solicitudes se asignan al grupo predeterminado siempre que no se puede clasificar la solicitud, o si hay otros errores de clasificación.
  
     Para más información, vea [Resource Governor Workload Group](../../relational-databases/resource-governor/resource-governor-workload-group.md) (Grupo de cargas de trabajo de Resource Governor) y [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).
  
## <a name="create-a-classification-function-for-machine-learning"></a>Crear una función de clasificación para el aprendizaje automático
  
Una función de clasificación examina las tareas entrantes y determina si la tarea se puede ejecutar con el grupo de recursos actual. Las tareas que no cumplen los criterios de la función de clasificación se vuelven a asignar al grupo de recursos predeterminado del servidor.
  
1. Empiece por especificar una función clasificadora que Resource Governor debe usar para determinar los grupos de recursos. Puede asignar un valor **null** como marcador de posición para la función clasificadora.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     Para obtener más información, vea [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).
  
2.  En la función clasificadora para cada grupo de recursos, defina el tipo de instrucciones o las solicitudes entrantes que se deben asignar al grupo de recursos.
  
     Por ejemplo, la siguiente función devuelve el nombre del esquema asignado al grupo de recursos externos definido por el usuario si la aplicación que envió la solicitud es "Microsoft R Host", "RStudio" o "Mashup". De lo contrario, devuelve el grupo de recursos predeterminado.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio', 'Mashup') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  Cuando se haya creado la función, vuelva a configurar el grupo de recursos para asignar la nueva función clasificadora al grupo de recursos externos que definió anteriormente.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>Comprobar los nuevos grupos de recursos y la afinidad

Para comprobar que se han realizado los cambios, debe comprobar la configuración de la memoria del servidor y la CPU de cada uno de los grupos de cargas de trabajo asociados con estos grupos de recursos de instancia:

+ el grupo predeterminado para el servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
+ el grupo de recursos predeterminado para procesos externos
+ el grupo definido por el usuario para procesos externos

1. Ejecute la siguiente instrucción para ver todos los grupos de cargas de trabajo:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **Ejemplo de resultados**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|interno|Media|25|0|0|0|0|1|2|
    |2|default|Media|25|0|0|0|0|2|2|
    |256|ds_wg|Media|25|0|0|0|0|2|256|
  
2.  Use la nueva vista de catálogo, [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para ver todos los grupos de recursos externos.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **Ejemplo de resultados**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|default|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     Para más información, vea [Resource Governor Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) (Vistas de catálogo de Resource Governor &#40;Transact-SQL&#41;).
  
3.  Ejecute la instrucción siguiente para devolver información sobre los recursos del equipo que tienen afinidad con el grupo de recursos externo, si procede:
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     En este caso, dado que los grupos se crearon con la afinidad AUTO, no se muestra ninguna información. Para más información, vea [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de la administración de recursos del servidor, vea:

+ [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) 
+ [Vistas de administración dinámica relacionadas con Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

Para obtener información general sobre la regulación de recursos para el aprendizaje automático, vea:

+ [Administrar cargas de trabajo de Python o R con Resource Governor en SQL Server Machine Learning Services](resource-governor.md)
