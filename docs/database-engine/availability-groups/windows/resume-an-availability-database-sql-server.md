---
title: "Reanudar una base de datos de disponibilidad (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "05/17/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.availabilitygroup.resumedatamove.f1"
helpviewer_keywords: 
  - "Grupos de disponibilidad [SQL Server], reanudar una base de datos"
  - "bases de datos secundarias [SQL Server], en el grupo de disponibilidad"
  - "bases de datos principales [SQL Server], en el grupo de disponibilidad"
  - "Grupos de disponibilidad [SQL Server], bases de datos"
ms.assetid: 20e9147b-e985-4caa-910e-fc4b38dbf9a1
caps.latest.revision: 38
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 38
---
# Reanudar una base de datos de disponibilidad (SQL Server)
  Puede reanudar una base de datos de disponibilidad suspendida en [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. La reanudación de una base de datos suspendida coloca la base de datos en el estado SYNCHRONIZING. La reanudación de la base de datos principal también reanuda cualquiera de las bases de datos secundarias suspendidas como resultado de suspender la base de datos principal. Si una base de datos secundaria se suspende localmente en la instancia de servidor que hospeda la réplica secundaria, esa base de datos secundaria se debe reanudar localmente. Una vez que una base de datos secundaria y la base de datos principal correspondiente están en el estado SYNCHRONIZING, se reanuda la sincronización de datos en la base de datos secundaria.  
  
> [!NOTE]  
>  Suspender y reanudar una base de datos secundaria de AlwaysOn no afecta directamente a la disponibilidad de la base de datos principal. Sin embargo, suspender una base de datos secundaria puede afectar a las capacidades de conmutación por error y redundancia de la base de datos principal, hasta que la base de datos secundaria suspendida se reanuda. Esto se diferencia del reflejo de base de datos, en el que el estado de reflejo se suspende tanto en la base de datos reflejada como en la base de datos principal hasta que el reflejo se reanuda. Al suspender una base de datos principal AlwaysOn, se suspende el movimiento de datos en todas las bases de datos secundarias y las capacidades de conmutación por error y redundancia cesan para esa base de datos hasta que la base de datos principal se reanuda.  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para reanudar una base de datos secundaria, mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
### Limitaciones y restricciones  
 Un comando RESUME realiza la devolución en cuanto haya sido aceptado por la réplica que hospeda la base de datos de destino, pero la reanudación real de la base de datos se produce de forma asincrónica.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe estar conectado a la instancia de servidor que hospeda la base de datos que se va a reanudar.  
  
-   El grupo de disponibilidad debe estar en línea.  
  
-   La base de datos principal debe estar en línea y disponible.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la base de datos.  
  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para reanudar una base de datos secundaria**  
  
1.  En el Explorador de objetos, conéctese a la instancia de servidor que hospeda la réplica de disponibilidad en la que desea reanudar una base de datos y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad**.  
  
3.  Expanda el grupo de disponibilidad.  
  
4.  Expanda el nodo **Bases de datos de disponibilidad**, haga clic con el botón derecho en la base de datos y haga clic en **Reanudar movimiento de datos**.  
  
5.  En el cuadro de diálogo **Reanudar movimiento de datos** , haga clic en **Aceptar**.  
  
> [!NOTE]  
>  Para reanudar bases de datos adicionales en esta ubicación de réplica, repita los pasos 4 y 5 para cada base de datos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para reanudar una base de datos secundaria suspendida localmente**  
  
1.  Conéctese a la instancia de servidor que hospeda la réplica secundaria cuya base de datos desea reanudar.  
  
2.  Reanude la base de datos secundaria utilizando la siguiente instrucción [ALTER DATABASE](../Topic/ALTER%20DATABASE%20SET%20HADR%20\(Transact-SQL\).md):  
  
     ALTER DATABASE *nombre_base_de_datos* SET HADR RESUME  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para reanudar una base de datos secundaria**  
  
1.  Cambie el directorio (**cd**) a la instancia del servidor que hospeda la réplica cuya base de datos quiere reanudar. Para obtener más información, vea [Requisitos previos](#Prerequisites), anteriormente en este tema.  
  
2.  Use el cmdlet **Resume-SqlAvailabilityDatabase** para reanudar el grupo de disponibilidad.  
  
     Por ejemplo, el comando siguiente reanuda la sincronización de datos para la base de datos de disponibilidad `MyDb3` en el grupo de disponibilidad `MyAg`.  
  
    ```  
    Resume-SqlAvailabilityDatabase `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\Databases\MyDb3  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet **Get-Help** en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de PowerShell de SQL Server](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Suspender una base de datos de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/suspend-an-availability-database-sql-server.md)  
  
## Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  