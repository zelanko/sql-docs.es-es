---
title: Cambio del modo de disponibilidad de una réplica para un grupo de disponibilidad
description: Una descripción de cómo cambiar el modo de disponibilidad de una réplica de disponibilidad dentro de un grupo de disponibilidad Always On mediante Transact-SQL (T-SQL), PowerShell o SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b1a3b5d1dfdf3a5e8556058cee750a4e2e08476a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "74822445"
---
# <a name="change-availability-mode-of-a-replica-within-an-always-on-availability-group"></a>Cambio del modo de disponibilidad de una réplica dentro de un grupo de disponibilidad AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo cambiar el modo de disponibilidad de una réplica de disponibilidad de un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] por medio de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell. El modo de disponibilidad es una propiedad de réplica que controla si la réplica se confirma asincrónica o sincrónicamente. El*modo confirmación asincrónica* maximiza el rendimiento a costa de la alta disponibilidad y solo admite la conmutación por error manual forzada (con posible pérdida de datos), que suele denominarse *conmutación por error forzada*. El*modo confirmación sincrónica* da prioridad a la alta disponibilidad sobre el rendimiento y, una vez sincronizada la réplica secundaria, admite la conmutación por error manual y, opcionalmente, la conmutación automática por error.  
    
##  <a name="Prerequisites"></a> Requisitos previos  
  
Debe estar conectado a la instancia del servidor que hospeda la réplica principal.  
  

##  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para cambiar el modo de disponibilidad de un grupo de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Haga clic en el grupo de disponibilidad cuya réplica desea cambiar.  
  
4.  Haga clic con el botón derecho en la réplica y haga clic en **Propiedades**.  
  
5.  En el cuadro de diálogo **Propiedades de réplica de disponibilidad** , use la lista desplegable **Modo de disponibilidad** para cambiar el modo de disponibilidad de esta réplica.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para cambiar el modo de disponibilidad de un grupo de disponibilidad**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *nombre_grupo* MODIFY REPLICA ON '*nombre_servidor*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     Donde *nombre_grupo* es el nombre del grupo de disponibilidad y *nombre_servidor* es el nombre de la instancia del servidor que hospeda la réplica que se va a modificar.  
  
    > [!NOTE]  
    >  FAILOVER_MODE = AUTOMATIC solo se admite si se especifica también AVAILABILITY_MODE = SYNCHRONOUS_COMMIT.  
  
     En el ejemplo siguiente, escrito en la réplica principal del grupo de disponibilidad `AccountsAG` , se cambian los modos de disponibilidad y de conmutación por error por confirmación sincrónica y conmutación automática por error, respectivamente, en la réplica que se hospeda en la instancia del servidor `INSTANCE09` .  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para cambiar el modo de disponibilidad de un grupo de disponibilidad**  
  
1.  Cambie el directorio (**cd**) a la instancia del servidor que hospeda la réplica principal.  
  
2.  Use el cmdlet **Set-SqlAvailabilityReplica** con el parámetro **AvailabilityMode** y, opcionalmente, el parámetro **FailoverMode** .  
  
     Por ejemplo, el comando siguiente modifica la réplica `MyReplica` en el grupo de disponibilidad `MyAg` para utilizar el modo de disponibilidad de confirmación sincrónica y admitir la conmutación automática por error.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet **Get-Help** en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Conmutación por error y modos de conmutación por error &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
