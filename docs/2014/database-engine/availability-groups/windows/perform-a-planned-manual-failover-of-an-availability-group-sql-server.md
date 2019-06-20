---
title: Realizar una conmutación por error manual planeada de un grupo de disponibilidad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.manualfailover.f1
helpviewer_keywords:
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 419f655d-3f9a-4e7d-90b9-f0bab47b3178
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 386e07bd1be4eaac4c75541665fc6951e2a24fd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789340"
---
# <a name="perform-a-planned-manual-failover-of-an-availability-group-sql-server"></a>Realizar una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)
  En este tema se describe cómo realizar una conmutación por error manual sin pérdida de datos (una *conmutación por error manual planeada*) en un grupo de disponibilidad AlwaysOn mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Un grupo de disponibilidad realiza la conmutación por error en el nivel de réplica de disponibilidad. Una conmutación por error manual planeada, como cualquier conmutación por error de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , realiza la transición de una réplica secundaria al rol principal y, simultáneamente, realiza la transición de la réplica principal anterior al rol secundario.  
  
 Una conmutación por error manual planeada, que solo se admite cuando la réplica principal y la réplica secundaria de destino se ejecutan en modo de confirmación sincrónica y están sincronizadas actualmente, conserva todos los datos de las bases de datos secundarias que están unidas al grupo de disponibilidad en la réplica secundaria de destino. Una vez que la réplica principal anterior realiza la transición al rol secundario, sus bases de datos se convierten en bases de datos secundarias y comienzan la sincronización con las nuevas bases de datos principales. Después de que todas realicen la transición al estado SYNCHRONIZED, la nueva réplica secundaria es apta para actuar como destino de una conmutación por error manual planeada futura.  
  
> [!NOTE]  
>  Si las replicas principal y secundaria se configuran para el modo de conmutación automática por error, una vez que la réplica secundaria esté sincronizada, también pueden actuar como destino de una conmutación automática por error. Para más información, vea [Modos de disponibilidad &#40;Grupos de disponibilidad AlwaysOn&#41;](availability-modes-always-on-availability-groups.md).  
  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Un comando de conmutación por error realiza la devolución en cuanto la réplica secundaria de destino haya aceptado el comando. Sin embargo, la recuperación de la base de datos se produce de forma asincrónica cuando el grupo de disponibilidad ha terminado la conmutación por error.  
  
-   La coherencia entre las bases de datos de las distintas bases de datos del grupo de disponibilidad no se mantiene en la conmutación por error.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] no admite las transacciones entre bases de datos ni las transacciones distribuidas. Para más información, vea [Transacciones entre bases de datos no compatibles para la creación de reflejo de la base de datos o grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](transactions-always-on-availability-and-database-mirroring.md).  
  
###  <a name="Prerequisites"></a> Requisitos previos y restricciones  
  
-   La réplica secundaria de destino y la réplica principal deben ejecutarse en modo de disponibilidad de confirmación sincrónica.  
  
-   La réplica secundaria de destino debe estar sincronizada actualmente con la réplica principal. Esto requiere que todas las bases de datos secundarias de la réplica secundaria deben estar unidas al grupo de disponibilidad y sincronizadas con sus bases de datos principales correspondientes (es decir, las bases de datos secundarias locales deben estar en estado SYNCHRONIZED).  
  
    > [!TIP]  
    >  Para determinar la preparación para la conmutación por error de una réplica secundaria, consulte la columna **is_failover_ready** de la vista de administración dinámica [sys.dm_hadr_database_cluster_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-cluster-states-transact-sql) o eche un vistazo a la columna **Preparación para la conmutación por error** del [Panel de grupo AlwaysOn](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
-   Esta tarea solo se admite en la réplica secundaria de destino. Debe estar conectado a la instancia del servidor que hospeda la réplica secundaria de destino.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para realizar la conmutación por error manual de un grupo de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a una instancia de servidor que hospede una réplica secundaria del grupo de disponibilidad que necesita ser objeto de conmutación por error, y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Haga clic con el botón secundario en el grupo de disponibilidad que va a ser objeto de conmutación por error y seleccione el comando **Conmutación por error** .  
  
4.  Esto inicia el Asistente para conmutación por error del grupo de disponibilidad. Para obtener más información, vea [Usar el Asistente para grupo de disponibilidad de conmutación por error &#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para realizar la conmutación por error manual de un grupo de disponibilidad**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica secundaria de destino.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *group_name* FAILOVER  
  
     donde *group_name* es el nombre del grupo de disponibilidad.  
  
     En el ejemplo siguiente se realiza manualmente una conmutación por error del grupo de disponibilidad *MyAg* a la réplica secundaria conectada.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg FAILOVER;  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para realizar la conmutación por error manual de un grupo de disponibilidad**  
  
1.  Cambie el directorio (`cd`) a la instancia de servidor que hospeda la réplica secundaria de destino.  
  
2.  Utilice el cmdlet `Switch-SqlAvailabilityGroup`.  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
     En el ejemplo siguiente, se realiza manualmente una conmutación por error del grupo de disponibilidad *MyAg* a la réplica secundaria que tiene la ruta de acceso especificada.  
  
    ```  
    Switch-SqlAvailabilityGroup -Path SQLSERVER:\Sql\SecondaryServer\InstanceName\AvailabilityGroups\MyAg  
    ```  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="FollowUp"></a> Seguimiento: Después de la conmutación manual por un grupo de disponibilidad  
 Si la conmutación por error se produjo fuera del grupo de disponibilidad de [!INCLUDE[ssFosAuto](../../../includes/ssfosauto-md.md)] , ajuste los votos de quórum de los nodos de WSFC para reflejar la configuración del nuevo grupo de disponibilidad. Para obtener más información, vea [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Conmutación por error y modos de conmutación por error &#40;grupos de disponibilidad AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [Realizar una conmutación por error manual forzada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
  
