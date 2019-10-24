---
title: Quitar una réplica secundaria de un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removesecondaryar.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], configuring
ms.assetid: 35ddc8b6-3e7c-4417-9a0a-d4987a09ddf7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b927483f5e57272460f1c2f0f1c4b1bca56a3abe
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782936"
---
# <a name="remove-a-secondary-replica-from-an-availability-group-sql-server"></a>Quitar una réplica secundaria de un grupo de disponibilidad (SQL Server)
  En este tema se describe cómo quitar una réplica secundaria de un grupo de disponibilidad AlwaysOn utilizando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para quitar una réplica secundaria, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Seguimiento:**  [después de quitar una réplica secundaria](#PostBestPractices)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Esta tarea solo se admite en la réplica principal.  
  
-   Solo se puede quitar una réplica secundaria de un grupo de disponibilidad.  
  
###  <a name="Prerequisites"></a> Prerequisites  
  
-   Debe estar conectado a la instancia del servidor que hospeda la réplica principal del grupo de disponibilidad.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para quitar una réplica secundaria**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Seleccione el grupo de disponibilidad y expanda el nodo **Réplicas de disponibilidad** .  
  
4.  Este paso depende de si desea quitar varias réplicas o solo una, del modo siguiente:  
  
    -   Para quitar varias réplicas, use el panel **Detalles del Explorador de objetos** para ver y seleccionar todas las réplicas que desea quitar. Para obtener más información, vea [Usar los detalles del Explorador de objetos para supervisar los grupos de disponibilidad &#40;SQL Server Management Studio&#41;](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   Para quitar una sola réplica, selecciónela en el panel **Explorador de objetos** o el panel **Detalles del Explorador de objetos** .  
  
5.  Haga clic con el botón derecho en la réplica o réplicas secundarias seleccionadas y seleccione **Quitar del grupo de disponibilidad** en el menú de comandos.  
  
6.  En el cuadro de diálogo **Quitar réplicas secundarias del grupo de disponibilidad** , para quitar todas las réplicas secundarias enumeradas, haga clic en **Aceptar**. Si no desea quitar todas las réplicas enumeradas, haga clic en **Cancelar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para quitar una réplica secundaria**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica principal.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE REPLICA ON '*instance_name*' [,...*n*]  
  
     donde *group_name* es el nombre del grupo de disponibilidad e *instance_name* es la instancia del servidor donde se encuentra la réplica secundaria.  
  
     En el ejemplo siguiente se quita una réplica secundaria del grupo de disponibilidad *MyAG* . La réplica secundaria de destino se encuentra en una instancia del servidor denominada *HADR_INSTANCE* en un equipo denominado *COMPUTER02*.  
  
    ```sql
    ALTER AVAILABILITY GROUP MyAG REMOVE REPLICA ON 'COMPUTER02\HADR_INSTANCE';  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para quitar una réplica secundaria**  
  
1.  Cambie el directorio (`cd`) a la instancia de servidor que hospeda la réplica principal.  
  
2.  Use el cmdlet **Remove-SqlAvailabilityReplica** .  
  
     Por ejemplo, el comando siguiente quita la réplica de disponibilidad en el servidor `MyReplica` del grupo de disponibilidad denominado `MyAg`.  Este comando debe ejecutarse en la instancia del servidor que hospeda la réplica principal del grupo de disponibilidad.  
  
    ```powershell
    Remove-SqlAvailabilityReplica -Path SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de PowerShell de SQL Server](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="PostBestPractices"></a> Seguimiento: después de quitar una réplica secundaria  
 Si especifica una réplica que no está actualmente disponible, cuando la réplica se ponga en línea, detectará que se ha quitado.  
  
 Quitar una réplica produce la detención de la recepción de datos Después de que una réplica secundaria confirma que se ha quitado del almacén global, la réplica quita la configuración del grupo disponibilidad de las bases de datos, que permanecen en la instancia del servidor local en estado RECOVERING.  
  
## <a name="see-also"></a>Ver también  
 [Información general de &#40;grupos de disponibilidad AlwaysOn&#41; SQL Server](overview-of-always-on-availability-groups-sql-server.md)    
 [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)   
 [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
