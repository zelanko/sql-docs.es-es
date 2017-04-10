---
title: "C&#243;mo: Crear un grupo de recursos para R | Microsoft Docs"
ms.custom: ""
ms.date: "10/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 19
---
# C&#243;mo: Crear un grupo de recursos para R
  Este tema describe cómo puede crear un grupo de recursos específicamente para administrar cargas de trabajo de R en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Se supone que ya se ha instalado servicios de R (en bases de datos) y desee volver a configurar el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instancia para admitir la administración más específica de los recursos que usa R.  
  
 Para obtener más información acerca de cómo administrar recursos de servidor, consulte [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md) y [relacionados Dynamic Management Views de regulador de recursos &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
 **Pasos**  
  
1.  Estado de revisión de los grupos de recursos existentes  
  
2.  Modificar grupos de recursos de servidor  
  
3.  Cree un nuevo grupo de recursos para los procesos externos  
  
4.  Cree una función de clasificación para identificar las solicitudes de R  
  
5.  Compruebe que está capturando los trabajos de R nuevo grupo de recursos externos  
  
##  <a name="bkmk_ReviewStatus"></a> Revisar el estado de los grupos de recursos existentes  
  
1.  En primer lugar, compruebe los recursos asignados al grupo predeterminado para el servidor.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **Resultado**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|predeterminados|0|100|0|100|100|0|0|  

2.  Compruebe los recursos asignados a los valores predeterminados **externo** grupo de recursos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **Resultado**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|predeterminados|100|20|0|2|  
 
3.  Con estos valores predeterminados de servidor, el tiempo de ejecución de R probable que tenga recursos insuficientes para completar la mayoría de las tareas. Para cambiar esta configuración, debe modificar el uso de recursos de servidor de la siguiente manera:  
  
    -   Reducir la memoria máxima del equipo que puede utilizarse por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   Aumente la memoria máxima del equipo que se puede utilizar el proceso externo  
  
## Modificar el uso de recursos de servidor  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la siguiente instrucción para limitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uso de memoria con **60%** del valor en la opción 'max server memory'.  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  De forma similar, ejecute la instrucción siguiente para limitar el uso de memoria por procesos externos a **40%** de recursos total del equipo.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  Para aplicar estos cambios, debe volver a configurar y reinicie el regulador de recursos como sigue:  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  Estos son sólo sugeridos opciones; debe evaluar los requisitos de R en comparación con otros procesos del servidor para determinar el equilibrio correcto para su entorno y la carga de trabajo.  
  
## Crear un grupo de recursos externos definidos por el usuario  
  
1.  Los cambios en la configuración del regulador de recursos se aplican en todo el servidor como un todo y afectan a las cargas de trabajo que utilizan los grupos predeterminados para el servidor, así como las cargas de trabajo que usan los grupos externos.  
  
     Por lo tanto, para proporcionar un mayor control sobre el que las cargas de trabajo deben tener prioridad, puede crear un nuevo grupo de recursos externos definido por el usuario. También debe definir una función de clasificación y asignar al grupo de recursos externos.  
  
     Empiece por crear un nuevo *grupo de recursos externos definidos por el usuario*. En el ejemplo siguiente, se denomina el grupo **ds_ep**.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     Tenga en cuenta el nuevo **EXTERNO** (palabra clave).  
  
2.  Crear un grupo de cargas de trabajo denominado `ds_wg` pueden utilizar para administrar solicitudes de sesión. Para las consultas SQL, usará el grupo predeterminado; proceso externo todas las consultas utilizarán el `ds_ep` grupo.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     Las solicitudes se asignan al grupo predeterminado siempre que no se puede clasificar la solicitud, o si hay otros errores de clasificación.  
  
     Para obtener más información, consulte [grupo de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md) y [CREATE WORKLOAD GROUP &#40; Transact-SQL &#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## Crear una función de clasificación para R  
  
1.  Una función de clasificación examina tareas entrantes y determina si la tarea es uno que se pueden ejecutar con el grupo de recursos actual. Tareas que no cumplen los criterios de la función de clasificación se asignan al grupo de recursos del servidor predeterminado.  
  
     Empiece por Especifica que una función clasificadora se debe utilizar el regulador de recursos para determinar los grupos de recursos. Puede asignar un valor null como marcador de posición para la función clasificadora.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     Para obtener más información, vea [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
2.  En la función clasificadora para cada grupo de recursos, defina el tipo de instrucciones o las solicitudes entrantes que se deben asignar al grupo de recursos.  
  
     Por ejemplo, la siguiente función devuelve el nombre del esquema asignado al grupo de recursos externos definidos por el usuario si la aplicación que envió la solicitud es 'Microsoft R Host' o 'RStudio'; de lo contrario, devuelve el grupo de recursos predeterminado.  
  
    ```  
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
  
3.  Cuando se ha creado la función, vuelva a configurar el grupo de recursos para asignar la nueva función clasificadora al grupo de recursos externos que definió anteriormente.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## Compruebe los nuevos grupos de recursos y afinidad  
  
1.  Para comprobar que se han realizado los cambios, compruebe la configuración de CPU y memoria del servidor para cada uno de los grupos de carga de trabajo asociados con todos los grupos de recursos de instancia: el grupo predeterminado para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] server, el grupo de recursos predeterminado para los procesos externos y el grupo definido por el usuario para procesos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **Resultado**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|GROUP_MAX_REQUESTS pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|interno|Media|25|0|0|0|0|1|2|  
    |2|predeterminados|Media|25|0|0|0|0|2|2|  
    |256|ds_wg|Media|25|0|0|0|0|2|256|  
  
2.  Puede utilizar la nueva vista de catálogo, [sys.resource_governor_external_resource_pools &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para ver todos los grupos de recursos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **Resultado**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|predeterminados|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     Para obtener más información, consulte [vistas de catálogo del regulador de recursos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
3.  La instrucción siguiente devuelve información acerca de los recursos del equipo que se establece para el grupo de recursos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     En este caso, dado que los grupos se crearon con afinidad AUTO, no se muestra ninguna información. Para obtener más información, consulte [sys.dm_resource_governor_resource_pool_affinity &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).  
  
## Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Regulador de recursos para servicios de R](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  