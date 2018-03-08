---
title: "Configurar la directiva de conmutación por error automática flexible | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e82b63c2bbc3d3788272f065d1cdb795decc8b1
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="configure-flexible-automatic-failover-policy"></a>Configurar la directiva de conmutación por error automática flexible
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo configurar la directiva de conmutación por error flexible para un grupo de disponibilidad AlwaysOn mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Una directiva de conmutación por error flexible proporciona mayor control sobre las condiciones que produce una conmutación automática por error para un grupo de disponibilidad. Al cambiar las condiciones de error que activan una conmutación automática por error y la frecuencia de comprobaciones de estado, se puede aumentar o reducir la probabilidad de una conmutación automática por error que sea compatible con su SLA por tener alta disponibilidad.  
  
-   **Antes de empezar:**  
  
     [Limitaciones de la conmutación automática por error](#Limitations)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la directiva flexible de conmutación por error mediante:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
    > [!NOTE]  
    >  La directiva flexible de conmutación por error de un grupo de disponibilidad no se puede configurar utilizando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Limitations"></a> Limitaciones de la conmutación automática por error  
  
-   Para que se produzca la conmutación automática por error, la réplica principal actual y una réplica secundaria deben estar configuradas para el modo de confirmación sincrónica con conmutación automática por error, y la réplica secundaria debe estar sincronizada con la réplica principal.  
  
-   Solo se admiten tres réplicas en la conmutación automática por error.  
  
-   Si un grupo de disponibilidad supera su umbral de error de WSFC, el clúster de WSFC no intentará una conmutación automática por error para dicho grupo. Además, el grupo de recursos de WSFC del grupo de disponibilidad permanece en un estado de error hasta que el administrador del clúster conecta manualmente el grupo de recursos con error o el administrador de la base de datos realiza una conmutación por error manual del grupo de disponibilidad. El *umbral de error de WSFC* se define como el número máximo de errores admitidos para el grupo de disponibilidad en un período de tiempo determinado. El período predeterminado es de seis horas, y el valor predeterminado del número máximo de errores durante este período es *n*-1, donde *n* es el número de nodos de WSFC. Para cambiar los valores del umbral de error de un grupo de disponibilidad determinado, use la consola del administrador de conmutación por error de WSFC.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
  
|Tarea|Permisos|  
|----------|-----------------|  
|Para configurar la directiva flexible de conmutación por error para un nuevo grupo de disponibilidad|Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
|Para modificar la directiva de un grupo de disponibilidad|Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para configurar la directiva flexible de conmutación por error**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Para un nuevo grupo de disponibilidad, use la instrucción [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Si va a modificar un grupo de disponibilidad existente, use la instrucción [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para establecer el nivel de la condición de conmutación por error, use la opción FAILURE_CONDITION_LEVEL = *n* , donde *n* es un entero entre 1 y 5.  
  
         Por ejemplo, la siguiente instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] cambia el nivel de condición de error de un grupo de disponibilidad existente, `AG1`, al nivel uno:  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         La relación de estos valores enteros con los niveles de condición de error es la siguiente:  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Level|La conmutación por error iniciada es automática cuando se produce…|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|Uno|Por inactividad de servidor. El servicio SQL Server se detiene debido a una conmutación por error o reinicio.|  
        |2|Dos|Al dejar de responder el servidor. Se cumple cualquier condición de un valor inferior, el servicio SQL Server se conecta al clúster y se supera el umbral del tiempo de espera de comprobación de estado, o la réplica principal actual está en un estado de error.|  
        |3|Tres|En errores de servidor críticos. Se cumple cualquier condición de un valor inferior o se produce un error de servidor crítico interno.<br /><br /> Es el nivel predeterminado.|  
        |4|Cuatro|En errores de servidor moderados. Se cumple cualquier condición de un valor inferior o se produce un error de servidor moderado.|  
        |5|Cinco|En cualquier condición de error apta. Se cumple cualquier condición de un valor inferior o se produce una condición de error adecuada.|  
  
         Para obtener más información sobre los niveles de condición de conmutación por error, vea [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
    -   Para configurar el umbral del tiempo de espera de comprobación de estado, use la opción HEALTH_CHECK_TIMEOUT = *n* , donde *n* es un entero de 15 000 milisegundos (15 segundos) a 4 294 967 295 milisegundos. El valor predeterminado es 30000 milisegundos (30 segundos).  
  
         Por ejemplo, la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] cambia el umbral de tiempo de espera de comprobación de estado de un grupo de disponibilidad disponible, `AG1`, 60.000 milisegundos (un minuto).  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para configurar la directiva flexible de conmutación por error**  
  
1.  Establezca el valor predeterminado (**cd**) en la instancia del servidor que hospeda la réplica principal.  
  
2.  Para agregar una réplica de disponibilidad a un grupo de disponibilidad, use el cmdlet **New-SqlAvailabilityGroup** . Para modificar una réplica de disponibilidad existente, use el cmdlet **Set-SqlAvailabilityGroup** .  
  
    -   Para establecer el nivel de condición de conmutación por error, use el parámetro **FailureConditionLevel***nivel*, donde *nivel* es uno de los siguientes valores:  
  
        |Valor|Level|La conmutación por error iniciada es automática cuando se produce…|  
        |-----------|-----------|-------------------------------------------|  
        |**OnServerDown**|Uno|Por inactividad de servidor. El servicio SQL Server se detiene debido a una conmutación por error o reinicio.|  
        |**OnServerUnresponsive**|Dos|Al dejar de responder el servidor. Se cumple cualquier condición de un valor inferior, el servicio SQL Server se conecta al clúster y se supera el umbral del tiempo de espera de comprobación de estado, o la réplica principal actual está en un estado de error.|  
        |**OnCriticalServerError**|Tres|En errores de servidor críticos. Se cumple cualquier condición de un valor inferior o se produce un error de servidor crítico interno.<br /><br /> Es el nivel predeterminado.|  
        |**OnModerateServerError**|Cuatro|En errores de servidor moderados. Se cumple cualquier condición de un valor inferior o se produce un error de servidor moderado.|  
        |**OnAnyQualifiedFailureConditions**|Cinco|En cualquier condición de error apta. Se cumple cualquier condición de un valor inferior o se produce una condición de error adecuada.|  
  
         Para obtener más información sobre los niveles de condición de conmutación por error, vea [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md).  
  
         Por ejemplo, el siguiente comando cambia el nivel de condición de error de un grupo de disponibilidad existente, `AG1`al nivel uno.  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `   
        -FailureConditionLevel OnServerDown  
        ```  
  
    -   Para establecer el umbral de tiempo de espera de comprobación de estado, use el parámetro **HealthCheckTimeout***n*, donde *n* es un entero de 15000 milisegundos (15 segundos) a 4294967295 milisegundos. El valor predeterminado es 30000 milisegundos (30 segundos).  
  
         Por ejemplo, el siguiente comando cambia el umbral de tiempo de espera de comprobación de estado de un grupo de disponibilidad disponible, `AG1`, a 120.000 milisegundos (dos minutos).  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
        -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  Para ver la sintaxis de un cmdlet, use el cmdlet **Get-Help** en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Conmutación por error y modos de conmutación por error &#40;Grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Directiva de conmutación por error para instancias de clústeres de conmutación por error](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
