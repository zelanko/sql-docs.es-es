---
title: Cambiar el modo de disponibilidad de una réplica de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: dafa6037682610d7011cdfc9f378ead6f95774fe
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782891"
---
# <a name="change-the-availability-mode-of-an-availability-replica-sql-server"></a>Cambiar el modo de disponibilidad de una réplica de disponibilidad (SQL Server)
  En este tema se describe cómo cambiar el modo de disponibilidad de una réplica de disponibilidad de un grupo de disponibilidad AlwaysOn en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell. El modo de disponibilidad es una propiedad de réplica que controla si la réplica se confirma asincrónica o sincrónicamente. El*modo confirmación asincrónica* maximiza el rendimiento a costa de la alta disponibilidad y solo admite la conmutación por error manual forzada (con posible pérdida de datos), que suele denominarse *conmutación por error forzada*. El*modo confirmación sincrónica* da prioridad a la alta disponibilidad sobre el rendimiento y, una vez sincronizada la réplica secundaria, admite la conmutación por error manual y, opcionalmente, la conmutación automática por error.  
  

  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Prerequisites  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
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
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) del siguiente modo:  
  
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

### <a name="to-change-the-availability-mode-of-an-availability-group"></a>Para cambiar el modo de disponibilidad de un grupo de disponibilidad
  
1.  Cambie el directorio (`cd`) a la instancia de servidor que hospeda la réplica principal.  
  
2.  Utilice el cmdlet `Set-SqlAvailabilityReplica` con el parámetro `AvailabilityMode` y, opcionalmente, el parámetro `FailoverMode`.  
  
     Por ejemplo, el comando siguiente modifica la réplica `MyReplica` en el grupo de disponibilidad `MyAg` para utilizar el modo de disponibilidad de confirmación sincrónica y admitir la conmutación automática por error.  
  
    ```powershell
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
     -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
Para configurar y usar el proveedor de SQL Server PowerShell, vea [proveedor de SQL Server PowerShell](../../../powershell/sql-server-powershell-provider.md).
  
## <a name="see-also"></a>Ver también  
 [Información general de &#40;grupos de disponibilidad AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Modos de disponibilidad (grupos de disponibilidad AlwaysOn)](availability-modes-always-on-availability-groups.md)    
 [Conmutación por error y &#40;modos de conmutación por error grupos de disponibilidad AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md)  
