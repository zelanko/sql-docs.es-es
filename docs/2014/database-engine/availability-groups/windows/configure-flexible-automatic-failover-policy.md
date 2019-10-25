---
title: Configuración de la Directiva de conmutación por error flexible para controlar las condiciones de la conmutación automática por error (Always On grupos de disponibilidad) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 452d3ac4dae2164fa0fa172528ae398ea91fed31
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797754"
---
# <a name="configure-the-flexible-failover-policy-to-control-conditions-for-automatic-failover-always-on-availability-groups"></a>Configurar la directiva de conmutación por error flexible para controlar las condiciones de la conmutación automática por error (grupos de disponibilidad AlwaysOn)
  En este tema se describe cómo configurar la directiva de conmutación por error flexible para un grupo de disponibilidad AlwaysOn mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Una directiva de conmutación por error flexible proporciona mayor control sobre las condiciones que produce una conmutación automática por error para un grupo de disponibilidad. Al cambiar las condiciones de error que activan una conmutación automática por error y la frecuencia de comprobaciones de estado, se puede aumentar o reducir la probabilidad de una conmutación automática por error que sea compatible con su SLA por tener alta disponibilidad.  
  
  
  
    > [!NOTE]  
    >  The flexible failover policy of an availability group cannot be configured by using [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Limitations"></a> Limitaciones de la conmutación automática por error  
  
-   Para que se produzca la conmutación automática por error, la réplica principal actual y una réplica secundaria deben estar configuradas para el modo de confirmación sincrónica con conmutación automática por error, y la réplica secundaria debe estar sincronizada con la réplica principal.  
  
-   Si un grupo de disponibilidad supera su umbral de error de WSFC, el clúster de WSFC no intentará una conmutación automática por error para dicho grupo. Además, el grupo de recursos de WSFC del grupo de disponibilidad permanece en un estado de error hasta que el administrador del clúster conecta manualmente el grupo de recursos con error o el administrador de la base de datos realiza una conmutación por error manual del grupo de disponibilidad. El *umbral de error de WSFC* se define como el número máximo de errores admitidos para el grupo de disponibilidad en un período de tiempo determinado. El período predeterminado es de seis horas, y el valor predeterminado del número máximo de errores durante este período es *n*-1, donde *n* es el número de nodos de WSFC. Para cambiar los valores del umbral de error de un grupo de disponibilidad determinado, use la consola del administrador de conmutación por error de WSFC.  
  
###  <a name="Prerequisites"></a> Prerequisites  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
  
|Tarea|Permissions|  
|----------|-----------------|  
|Para configurar la directiva flexible de conmutación por error para un nuevo grupo de disponibilidad|Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
|Para modificar la directiva de un grupo de disponibilidad|Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.|  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para configurar la directiva flexible de conmutación por error**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Para un nuevo grupo de disponibilidad, use la instrucción [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] . Si va a modificar un grupo de disponibilidad existente, use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] .  
  
    -   Para establecer el nivel de la condición de conmutación por error, use la opción FAILURE_CONDITION_LEVEL = *n* , donde *n* es un entero entre 1 y 5.  
  
         Por ejemplo, la siguiente instrucción de [!INCLUDE[tsql](../../../includes/tsql-md.md)] cambia el nivel de condición de error de un grupo de disponibilidad existente, `AG1`, al nivel uno:  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         La relación de estos valores enteros con los niveles de condición de error es la siguiente:  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|level|La conmutación por error iniciada es automática cuando se produce...|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|Uno|Por inactividad de servidor. El servicio SQL Server se detiene debido a una conmutación por error o reinicio.|  
        |2|Dos|Al dejar de responder el servidor. Se cumple cualquier condición de un valor inferior, el servicio SQL Server se conecta al clúster y se supera el umbral del tiempo de espera de comprobación de estado, o la réplica principal actual está en un estado de error.|  
        |3|Tres|En errores de servidor críticos. Se cumple cualquier condición de un valor inferior o se produce un error de servidor crítico interno.<br /><br /> Es el nivel predeterminado.|  
        |4|Cuatro|En errores de servidor moderados. Se cumple cualquier condición de un valor inferior o se produce un error de servidor moderado.|  
        |5|Cinco|En cualquier condición de error apta. Se cumple cualquier condición de un valor inferior o se produce una condición de error adecuada.|  
  
         Para obtener más información sobre los niveles de condición de conmutación por error, vea [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md).  
  
    -   Para configurar el umbral del tiempo de espera de comprobación de estado, use la opción HEALTH_CHECK_TIMEOUT = *n* , donde *n* es un entero de 15 000 milisegundos (15 segundos) a 4 294 967 295 milisegundos. El valor predeterminado es 30000 milisegundos (30 segundos).  
  
         Por ejemplo, la siguiente instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] cambia el umbral de tiempo de espera de comprobación de estado de un grupo de disponibilidad disponible, `AG1`, 60.000 milisegundos (un minuto).  
  
        ```sql
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  

### <a name="to-configure-the-flexible-failover-policy"></a>Para configurar la Directiva de conmutación por error flexible * *  
  
1.  Establezca el valor predeterminado (`cd`) en la instancia del servidor que hospeda la réplica de disponibilidad principal.  
  
2.  Para agregar una réplica de disponibilidad a un grupo de disponibilidad, use el cmdlet `New-SqlAvailabilityGroup`. Para modificar una réplica de disponibilidad existente, use el cmdlet `Set-SqlAvailabilityGroup`.  
  
    -   Para establecer el nivel de la condición de conmutación por error, use el parámetro de *nivel* de `FailureConditionLevel`, donde, *LEVEL* es uno de los siguientes valores:  
  
        |Value|level|La conmutación por error iniciada es automática cuando se produce...|  
        |-----------|-----------|-------------------------------------------|  
        |`OnServerDown`|Uno|Por inactividad de servidor. El servicio SQL Server se detiene debido a una conmutación por error o reinicio.|  
        |`OnServerUnresponsive`|Dos|Al dejar de responder el servidor. Se cumple cualquier condición de un valor inferior, el servicio SQL Server se conecta al clúster y se supera el umbral del tiempo de espera de comprobación de estado, o la réplica principal actual está en un estado de error.|  
        |`OnCriticalServerError`|Tres|En errores de servidor críticos. Se cumple cualquier condición de un valor inferior o se produce un error de servidor crítico interno.<br /><br /> Es el nivel predeterminado.|  
        |`OnModerateServerError`|Cuatro|En errores de servidor moderados. Se cumple cualquier condición de un valor inferior o se produce un error de servidor moderado.|  
        |`OnAnyQualifiedFailureConditions`|Cinco|En cualquier condición de error apta. Se cumple cualquier condición de un valor inferior o se produce una condición de error adecuada.|  
  
         Para obtener más información sobre los niveles de condición de conmutación por error, vea [Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad &#40;SQL Server&#41;](flexible-automatic-failover-policy-availability-group.md).  
  
         Por ejemplo, el siguiente comando cambia el nivel de condición de error de un grupo de disponibilidad existente, `AG1`al nivel uno.  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `
         -FailureConditionLevel OnServerDown  
        ```  
  
    -   Para establecer el umbral de tiempo de espera de comprobación de estado, use el parámetro `HealthCheckTimeout`*n* , donde *n* es un entero de 15000 milisegundos (15 segundos) a 4294967295 milisegundos. El valor predeterminado es 30000 milisegundos (30 segundos).  
  
         Por ejemplo, el siguiente comando cambia el umbral de tiempo de espera de comprobación de estado de un grupo de disponibilidad disponible, `AG1`, a 120.000 milisegundos (dos minutos).  
  
        ```powershell
        Set-SqlAvailabilityGroup `
         -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `
         -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de PowerShell de SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Obtener ayuda de SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
## <a name="see-also"></a>Ver también  
 [Información general de &#40;grupos de disponibilidad AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Modos de disponibilidad (grupos de disponibilidad AlwaysOn)](availability-modes-always-on-availability-groups.md)    
 [Conmutación por error y &#40;modos&#41; de conmutación por error grupos de disponibilidad AlwaysOn](failover-and-failover-modes-always-on-availability-groups.md)    
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Directiva de conmutación por error para instancias de clústeres de conmutación por error](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
