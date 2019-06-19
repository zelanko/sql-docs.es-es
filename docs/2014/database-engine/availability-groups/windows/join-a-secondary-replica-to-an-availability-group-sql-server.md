---
title: Combinar una réplica secundaria con un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.joinreplica.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], joining
- Availability Groups [SQL Server], configuring
ms.assetid: e5bd2489-097a-490e-8ea1-34fe48378ad1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f667ff368ca54f2ccfaeab47716338c7d694c1da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62792161"
---
# <a name="join-a-secondary-replica-to-an-availability-group-sql-server"></a>Combinar una réplica secundaria con un grupo de disponibilidad (SQL Server)
  En este tema se describe cómo combinar una réplica secundaria con un grupo de disponibilidad de AlwaysOn mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Después de agregar una réplica secundaria a un grupo de disponibilidad de AlwaysOn, la réplica secundaria se debe combinar con el grupo de disponibilidad. La operación de combinar una réplica se debe realizar en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda la réplica secundaria.  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para preparar una base de datos secundaria, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Seguimiento:** [Configurar las bases de datos secundarias](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   La réplica principal del grupo de disponibilidad debe estar en línea.  
  
-   Debe estar conectado a la instancia del servidor que hospede una réplica secundaria que no se haya unido todavía al grupo de disponibilidad.  
  
-   La instancia del servidor local debe poder conectarse al extremo de creación de reflejo de la base de datos de la instancia del servidor que hospeda la réplica principal.  
  
> [!IMPORTANT]  
>  Si no se cumple ningún requisito previo, la operación de unión produce un error. Después de un intento de unión frustrado, puede ser necesario conectarse a la instancia de servidor que hospeda la réplica principal para quitar y volver a agregar la réplica secundaria antes de unirla al grupo de disponibilidad. Para obtener más información, vea [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md) y [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para combinar una réplica de disponibilidad con un grupo de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica secundaria y haga clic en el nombre del servidor para expandir el árbol de servidores.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Seleccione el grupo de disponibilidad de la réplica secundaria a la que está conectado.  
  
4.  Haga clic con el botón derecho en la réplica secundaria y haga clic en **Combinar con grupo de disponibilidad**.  
  
5.  Se abrirá el cuadro de diálogo **Combinar réplica con grupo de disponibilidad** .  
  
6.  Para combinar la réplica secundaria con el grupo de disponibilidad, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para combinar una réplica de disponibilidad con un grupo de disponibilidad**  
  
1.  Conéctese a la instancia del servidor que hospeda la réplica secundaria.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *group_name* JOIN  
  
     donde *group_name* es el nombre del grupo de disponibilidad.  
  
     En el ejemplo siguiente se une la réplica secundaria al grupo de disponibilidad `MyAG`.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAG JOIN;  
    ```  
  
    > [!NOTE]  
    >  Para ver esta instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] usada en contexto, vea [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md).  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell  
 **Para combinar una réplica de disponibilidad con un grupo de disponibilidad**  
  
 En el proveedor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell:  
  
1.  Cambie el directorio (`cd`) a la instancia del servidor que hospeda la réplica secundaria.  
  
2.  Combine la réplica secundaria con el grupo de disponibilidad ejecutando el cmdlet **Join-SqlAvailabilityGroup** con el nombre del grupo de disponibilidad.  
  
     Por ejemplo, el comando siguiente une una réplica secundaria hospedada en la instancia de servidor que se encuentra en la ruta especificada al grupo de disponibilidad denominado `MyAg`.  Esta instancia de servidor debe hospedar una replicación secundaria en este grupo de disponibilidad.  
  
    ```  
    Join-SqlAvailabilityGroup -Path SQLSERVER:\SQL\SecondaryServer\InstanceName -Name 'MyAg'  
    ```  
  
    > [!NOTE]  
    >  Para ver la sintaxis de un cmdlet, use el cmdlet `Get-Help` en el entorno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
 **Para configurar y usar el proveedor de SQL Server PowerShell**  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="FollowUp"></a> Seguimiento: Configurar las bases de datos secundarias  
 Para cada base de datos del grupo de disponibilidad se necesita una base de datos secundaria en la instancia del servidor que hospeda la réplica secundaria. Puede configurar las bases de datos secundarias antes o después de unir una réplica secundaria a un grupo de disponibilidad del modo siguiente:  
  
1.  Restaure la base de datos y las copias de seguridad de registros recientes de cada base de datos principal en la instancia del servidor que hospeda la réplica secundaria, utilizando RESTORE WITH NORECOVERY para cada operación de restauración. Para obtener más información, vea [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
2.  Una cada base de datos secundaria al grupo de disponibilidad. Para obtener más información, vea [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Creación y configuración de grupos de disponibilidad &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Solución de problemas de configuración de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;eliminado](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
