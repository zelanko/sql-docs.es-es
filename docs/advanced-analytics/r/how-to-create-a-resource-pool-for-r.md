---
title: "Cómo: Crear un grupo de recursos para R | Microsoft Docs"
ms.custom: 
ms.date: 10/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c7f7f6e4-774d-4b45-b94a-f06c51718475
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: be3afb3a1ff5175fbb3d0735cde59bd19bb47f6c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="how-to-create-a-resource-pool-for-r"></a>Cómo: Crear un grupo de recursos para R
  En este tema se describe cómo se puede crear un grupo de recursos específicamente para administrar cargas de trabajo de R en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Se supone que ya ha instalado R Services (En base de datos) y quiere volver a configurar la instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para admitir la administración más específica de los recursos que usa R.  
  
 Para más información sobre cómo administrar recursos de servidor, vea [Resource Governor](../../relational-databases/resource-governor/resource-governor.md) y [Resource Governor Related Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md) (Vistas de administración dinámica relacionadas con Resource Governor &#40;Transact-SQL&#41;).  
  
 **Pasos**  
  
1.  Estado de revisión de los grupos de recursos existentes  
  
2.  Modificar grupos de recursos de servidor  
  
3.  Crear un nuevo grupo de recursos para los procesos externos  
  
4.  Crear una función de clasificación para identificar las solicitudes de R  
  
5.  Comprobar que el nuevo grupo de recursos externos está capturando los trabajos de R  
  
##  <a name="bkmk_ReviewStatus"></a> Estado de revisión de los grupos de recursos existentes  
  
1.  En primer lugar, compruebe los recursos asignados al grupo predeterminado para el servidor.  
  
    ```  
    SELECT * FROM sys.resource_governor_resource_pools WHERE name = 'default'  
    ```  
     **Resultado**

    |pool_id|name|min_cpu_percent|max_cpu_percent|min_memory_percent|max_memory_percent|cap_cpu_percent|min_iops_per_volume|max_iops_per_volume|  
    |-|-|-|-|-|-|-|-|-|  
    |2|predeterminados|0|100|0|100|100|0|0|  

2.  Compruebe los recursos asignados al grupo de recursos **externos** predeterminado.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools WHERE name = 'default'  
    ```  
     
    **Resultado**

    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|predeterminados|100|20|0|2|  
 
3.  Con estos valores predeterminados de servidor, es probable que el tiempo de ejecución de R no tenga recursos suficientes para completar la mayoría de las tareas. Para cambiar esta configuración, se debe modificar el uso de recursos de servidor de la siguiente manera:  
  
    -   Reducir la memoria máxima del equipo que puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
    -   Aumentar la memoria máxima del equipo que puede usar el proceso externo  
  
## <a name="modify-server-resource-usage"></a>Modificar el uso de recursos de servidor  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ejecute la siguiente instrucción para limitar el uso de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al **60 %** del valor de la opción "max server memory".  
  
    ```  
    ALTER RESOURCE POOL "default" WITH (max_memory_percent = 60);  
    ```  
  
2.  De forma similar, ejecute la instrucción siguiente para limitar el uso de memoria de los procesos externos al **40 %** de los recursos totales del equipo.  
  
    ```  
    ALTER EXTERNAL RESOURCE POOL "default" WITH (max_memory_percent = 40);  
    ```  
  
3.  Para aplicar estos cambios, debe volver a configurar y reiniciar Resource Governor de esta forma:  
  
    ```  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
    > [!NOTE]  
    >  Estas son solo opciones sugeridas. Debe evaluar los requisitos de R en comparación con otros procesos del servidor para determinar el equilibrio correcto para el entorno y la carga de trabajo.  
  
## <a name="create-a-user-defined-external-resource-pool"></a>Crear un grupo de recursos externos definido por el usuario  
  
1.  Los cambios en la configuración de Resource Governor se aplican en todo el servidor como un todo y afectan a las cargas de trabajo que usan los grupos predeterminados para el servidor, así como a las cargas de trabajo que usan los grupos externos.  
  
     Por tanto, para proporcionar un mayor control sobre qué cargas de trabajo deben tener prioridad, puede crear un nuevo grupo de recursos externos definido por el usuario. También debe definir una función de clasificación y asignarla al grupo de recursos externos.  
  
     Empiece por crear un nuevo *grupo de recursos externos definido por el usuario*. En el ejemplo siguiente, el grupo se denomina **ds_ep**.  
  
    ```  
    CREATE EXTERNAL RESOURCE POOL ds_ep WITH (max_memory_percent = 40);  
    ```  
  
     Observe la nueva palabra clave **EXTERNAL**.  
  
2.  Cree un grupo de cargas de trabajo denominado `ds_wg` para usar en la administración de solicitudes de sesión. Para las consultas SQL, usará el grupo predeterminado. Para las consultas de procesos externos usará el grupo `ds_ep`.  
  
    ```  
    CREATE WORKLOAD GROUP ds_wg WITH (importance = medium) USING "default", EXTERNAL "ds_ep";  
    ```  
  
     Las solicitudes se asignan al grupo predeterminado siempre que no se puede clasificar la solicitud, o si hay otros errores de clasificación.  
  
     Para más información, vea [Resource Governor Workload Group](../../relational-databases/resource-governor/resource-governor-workload-group.md) (Grupo de cargas de trabajo de Resource Governor) y [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## <a name="create-a-classification-function-for-r"></a>Crear una función de clasificación para R  
  
1.  Una función de clasificación examina las tareas entrantes y determina si la tarea se puede ejecutar con el grupo de recursos actual. Las tareas que no cumplen los criterios de la función de clasificación se vuelven a asignar al grupo de recursos predeterminado del servidor.  
  
     Empiece por especificar una función clasificadora que Resource Governor debe usar para determinar los grupos de recursos. Puede asignar un valor NULL como marcador de posición para la función clasificadora.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH (classifier_function = NULL);  
    ALTER RESOURCE GOVERNOR reconfigure;  
    ```  
  
     Para obtener más información, vea [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).  
  
2.  En la función clasificadora para cada grupo de recursos, defina el tipo de instrucciones o las solicitudes entrantes que se deben asignar al grupo de recursos.  
  
     Por ejemplo, la siguiente función devuelve el nombre del esquema asignado al grupo de recursos externos definido por el usuario si la aplicación que envió la solicitud es "Microsoft R Host" o "RStudio". De lo contrario, devuelve el grupo de recursos predeterminado.  
  
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
  
3.  Cuando se haya creado la función, vuelva a configurar el grupo de recursos para asignar la nueva función clasificadora al grupo de recursos externos que definió anteriormente.  
  
    ```  
    ALTER RESOURCE GOVERNOR WITH  (classifier_function = dbo.is_ds_apps);  
    ALTER RESOURCE GOVERNOR WITH reconfigure;  
    go  
    ```  
  
## <a name="verify-new-resource-pools-and-affinity"></a>Comprobar los nuevos grupos de recursos y la afinidad  
  
1.  Para comprobar que se han realizado los cambios, compruebe la configuración de CPU y memoria del servidor para cada uno de los grupos de carga de trabajo asociados con todos los grupos de recursos de instancia: el grupo predeterminado para el servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el grupo de recursos predeterminado para los procesos externos y el grupo definido por el usuario para los procesos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_workload_groups;  
    ```  

    **Resultado**

    |group_id|name|importance|request_max_memory_grant_percent|request_max_cpu_time_sec|request_memory_grant_timeout_sec|max_dop|group_max_requests pool_id|pool_idd|external_pool_idd|  
    |-|-|-|-|-|-|-|-|-|-|  
    |1|interno|Media|25|0|0|0|0|1|2|  
    |2|predeterminados|Media|25|0|0|0|0|2|2|  
    |256|ds_wg|Media|25|0|0|0|0|2|256|  
  
2.  Puede usar la nueva vista de catálogo, [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md), para ver todos los grupos de recursos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pools;  
    ```  
    **Resultado**
    
    |external_pool_id|name|max_cpu_percent|max_memory_percent|max_processes|version|  
    |-|-|-|-|-|-|  
    |2|predeterminados|100|20|0|2|  
    |256|ds_ep|100|40|0|1|  
  
     Para más información, vea [Resource Governor Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md) (Vistas de catálogo de Resource Governor &#40;Transact-SQL&#41;).  
  
3.  La instrucción siguiente devuelve información sobre los recursos del equipo que se asocian al grupo de recursos externos.  
  
    ```  
    SELECT * FROM sys.resource_governor_external_resource_pool_affinity;  
    ```  
  
     En este caso, dado que los grupos se crearon con la afinidad AUTO, no se muestra ninguna información. Para más información, vea [sys.dm_resource_governor_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pool-affinity-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Regulación de recursos para R Services](../../advanced-analytics/r-services/resource-governance-for-r-services.md)  
  
  

