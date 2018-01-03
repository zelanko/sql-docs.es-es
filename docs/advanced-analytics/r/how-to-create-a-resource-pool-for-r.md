---
title: "Crear un grupo de recursos para el aprendizaje automático | Documentos de Microsoft"
ms.custom: 
ms.date: 11/13/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f5699ed583f0fd40657f3be5f132b879681a7942
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="create-a-resource-pool-for-machine-learning"></a>Crear un grupo de recursos para el aprendizaje automático

Este tema describe cómo puede crear un grupo de recursos específicamente para administrar cargas de trabajo de aprendizaje de máquina en SQL Server. Se supone que ya ha instalado y habilitado el características, de aprendizaje automático y volver a configurar la instancia para admitir la administración específica más de los recursos utilizados por un proceso externo, como R o Python.

El proceso incluye varios pasos:

1.  Revise el estado de los grupos de recursos existente. Es importante que sepa qué servicios están usando recursos existentes.
2.  Modificar grupos de recursos de servidor.
3.  Crear un nuevo grupo de recursos para los procesos externos.
4.  Crear una función de clasificación para identificar las solicitudes de script externo.
5.  Compruebe que el nuevo grupo de recursos externo está capturando los trabajos de R o Python desde las cuentas o los clientes especificados.

**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] y [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)][!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

##  <a name="bkmk_ReviewStatus"></a> Estado de revisión de los grupos de recursos existentes
  
1.  Utilice una instrucción como la siguiente para comprobar los recursos asignados al grupo predeterminado para el servidor.
  
    ```sql
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'
    ```

    **Resultados del ejemplo**

    |pool_id|NAME|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|
    |-|-|-|-|-|-|-|-|-|
    |2|predeterminados|0|100|0|100|100|0|0|

2.  Compruebe los recursos asignados al grupo de recursos **externos** predeterminado.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'
    ```

    **Resultados del ejemplo**

    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|predeterminados|100|20|0|2|
 
3.  En estos valores predeterminados de servidor, el tiempo de ejecución externo probable que tenga recursos insuficientes para completar la mayoría de las tareas. Para cambiar esta configuración, se debe modificar el uso de recursos de servidor de la siguiente manera:
  
    -   Reducir la memoria máxima del equipo que se puede usar el motor de base de datos.
  
    -   Aumente la memoria máxima del equipo que se puede usar el proceso externo.

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
    >  Estos son los valores sugeridos simplemente para iniciar con; se debe evaluar sus tareas a la luz de otros procesos del servidor para determinar el equilibrio correcto para su entorno y la carga de trabajo de aprendizaje automático.

## <a name="create-a-user-defined-external-resource-pool"></a>Crear un grupo de recursos externos definido por el usuario
  
1.  Los cambios en la configuración de Resource Governor se aplican en todo el servidor como un todo y afectan a las cargas de trabajo que usan los grupos predeterminados para el servidor, así como a las cargas de trabajo que usan los grupos externos.
  
     Por tanto, para proporcionar un mayor control sobre qué cargas de trabajo deben tener prioridad, puede crear un nuevo grupo de recursos externos definido por el usuario. También debe definir una función de clasificación y asignarla al grupo de recursos externos. El **externo** palabra clave es nuevo.
  
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
  
1. Comience por Especifica que una función clasificadora se debe utilizar el regulador de recursos para determinar los grupos de recursos. Puede asignar un **null** como un marcador de posición para la función clasificadora.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);
    ALTER RESOURCE GOVERNOR RECONFIGURE;
    ```
  
     Para obtener más información, vea [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).
  
2.  En la función clasificadora para cada grupo de recursos, defina el tipo de instrucciones o las solicitudes entrantes que se deben asignar al grupo de recursos.
  
     Por ejemplo, la siguiente función devuelve el nombre del esquema asignado al grupo de recursos externos definido por el usuario si la aplicación que envió la solicitud es "Microsoft R Host" o "RStudio". De lo contrario, devuelve el grupo de recursos predeterminado.
  
    ```sql
    USE master
    GO
    CREATE FUNCTION is_ds_apps()
    RETURNS sysname
    WITH schemabinding
    AS
    BEGIN
        IF program_name() in ('Microsoft R Host', 'RStudio') RETURN 'ds_wg';
        RETURN 'default'
        END;
    GO
    ```
  
3.  Cuando se haya creado la función, vuelva a configurar el grupo de recursos para asignar la nueva función clasificadora al grupo de recursos externos que definió anteriormente.
  
    ```sql
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);
    ALTER RESOURCE GOVERNOR WITH reconfigure;
    GO
    ```

## <a name="verify-new-resource-pools-and-affinity"></a>Comprobar los nuevos grupos de recursos y la afinidad

Para comprobar que se han realizado los cambios, debe comprobar la configuración de CPU y memoria del servidor para cada uno de los grupos de cargas de trabajo asociados a estos grupos de recursos de instancia:

+ el grupo predeterminado para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server
+ el grupo de recursos predeterminado para los procesos externos
+ el grupo definido por el usuario para los procesos externos

1. Ejecute la instrucción siguiente para ver todos los grupos de carga de trabajo:

    ```sql
    SELECT * FROM sys.resource_governor_workload_groups;
    ```

    **Resultados del ejemplo**

    |group_id|NAME|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_id|
    |-|-|-|-|-|-|-|-|-|-|
    |1|interno|Media|25|0|0|0|0|1|2|
    |2|predeterminados|Media|25|0|0|0|0|2|2|
    |256|ds_wg|Media|25|0|0|0|0|2|256|
  
2.  Use la nueva vista de catálogo, [sys.resource_governor_external_resource_pools &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para ver todos los grupos de recursos externos.
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pools;
    ```

    **Resultados del ejemplo**
    
    |external_pool_id|NAME|max_cpu_percent|max_memory_percent|max_processes|version|
    |-|-|-|-|-|-|
    |2|predeterminados|100|20|0|2|
    |256|ds_ep|100|40|0|1|
  
     Para más información, vea [Resource Governor Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) (Vistas de catálogo de Resource Governor &#40;Transact-SQL&#41;).
  
3.  Ejecute la siguiente instrucción para devolver información acerca de los recursos del equipo que se ha establecido la afinidad para el grupo de recursos externos, si corresponde:
  
    ```sql
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;
    ```
  
     En este caso, dado que los grupos se crearon con la afinidad AUTO, no se muestra ninguna información. Para más información, vea [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).

## <a name="see-also"></a>Vea también

Para obtener más información acerca de cómo administrar los recursos del servidor, vea:

+  [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) 
+ [Regulador de recursos relacionados con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)

Para obtener información general de la regulación de recursos para el aprendizaje automático, vea:

+  [Regulador de recursos para servicios de aprendizaje de máquina](../../advanced-analytics/r/resource-governance-for-r-services.md)
