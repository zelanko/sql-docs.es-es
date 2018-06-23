---
title: Crear un grupo de disponibilidad (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
caps.latest.revision: 39
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 9d02bd4202848c0c22033b00d818c2f0d2554bc2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112340"
---
# <a name="create-an-availability-group-sql-server-powershell"></a>Crear un grupo de disponibilidad (SQL Server PowerShell)
  En este tema se describe cómo usar los cmdlets de PowerShell para crear y configurar un grupo de disponibilidad de AlwaysOn mediante PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Un *grupo de disponibilidad* define un conjunto de bases de datos de usuario que realizarán la conmutación por error como una sola unidad y un conjunto de asociados de conmutación por error, conocido como *réplicas de disponibilidad*, que admiten la conmutación por error.  
  
> [!NOTE]  
>  Para obtener una introducción a los grupos de disponibilidad, vea [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md).  
  

  
> [!NOTE]  
>  Como alternativa al uso de cmdlets de PowerShell, puede usar el asistente Crear grupo de disponibilidad o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para obtener más información, vea [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md) o [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Se recomienda encarecidamente leer esta sección antes de intentar crear el primer grupo de disponibilidad.  
  
###  <a name="PrerequisitesRestrictions"></a> Requisitos previos, restricciones y recomendaciones  
  
-   Antes de crear un grupo de disponibilidad, compruebe que cada una de las instancias host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] reside en un nodo de clúster de conmutación por error de Windows Server (WSFC) diferente en el mismo clúster de conmutación por error de WSFC. Además, compruebe que las instancias del servidor cumplen con los otros requisitos previos de la instancia del servidor, que se cumplen todos los demás requisitos de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y que es consciente de las recomendaciones. Para más información, recomendamos encarecidamente que lea [Requisitos previos, restricciones y recomendaciones para grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Se requiere la pertenencia al rol fijo de servidor **sysadmin** y el permiso de servidor CREATE AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
###  <a name="SummaryPSStatements"></a> Resumen de tareas y cmdlets de PowerShell correspondientes  
 En la siguiente tabla se enumeran las tareas básicas relacionadas con la configuración de un grupo de disponibilidad y se indican las que son compatibles con cmdlets de PowerShell. Las tareas de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] se deben realizar en la secuencia en que se muestran en la tabla.  
  
|Tarea|Cmdlets de PowerShell (si hay disponibles) o instrucción Transact-SQL|Dónde realizar la tarea**<sup>*</sup>**|  
|----------|--------------------------------------------------------------------|-------------------------------------------|  
|Crear extremo de creación de reflejo de la base de datos (una vez por instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] )|`New-SqlHadrEndPoint`|Se ejecuta en cada instancia del servidor que carece de extremo de creación de reflejo de la base de datos.<br /><br /> Nota: Para modificar un extremo de reflejo de base de datos existente, use `Set-SqlHadrEndpoint`.|  
|Crear grupo de disponibilidad|Primero, utilice el cmdlet `New-SqlAvailabilityReplica` con el parámetro `-AsTemplate` para crear un objeto de réplica de disponibilidad en memoria para cada una de las dos réplicas de disponibilidad que va a incluir en el grupo de disponibilidad.<br /><br /> A continuación, cree el grupo de disponibilidad mediante el uso de la `New-SqlAvailabilityGroup` cmdlet y hacer referencia a los objetos de réplica de disponibilidad.|Se ejecuta en la instancia del servidor que va a hospedar la réplica principal inicial.|  
|Unir la réplica secundaria al grupo de disponibilidad|`Join-SqlAvailabilityGroup`|Se ejecuta en cada una de las instancias del servidor que hospeda una réplica secundaria.|  
|Preparar la base de datos secundaria|`Backup-SqlDatabase` y `Restore-SqlDatabase`|Se crean las copias de seguridad de la instancia del servidor que hospeda la réplica principal.<br /><br /> Se restauran las copias de seguridad de cada una de las instancias del servidor que hospedan una réplica de secundaria mediante el parámetro de restauración `NoRecovery`. Si las rutas de acceso de archivo difieren entre equipos que hospedan la réplica principal y la réplica secundaria de destino, utilice también el parámetro de restauración `RelocateFile`.|  
|Iniciar la sincronización de datos uniendo cada base de datos secundaria al grupo de disponibilidad|`Add-SqlAvailabilityDatabase`|Se ejecuta en cada una de las instancias del servidor que hospedan una réplica secundaria.|  
  
 **<sup>*</sup>**  Para llevar a cabo una tarea determinada, cambie el directorio (`cd`) a la instancia del servidor indicado o instancias.  
  
###  <a name="PsProviderLinks"></a> Para configurar y usar el proveedor de SQL Server PowerShell  
  
-   [Proveedor de SQL Server PowerShell Provider](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
##  <a name="PowerShellProcedure"></a> Usar PowerShell para crear y configurar un grupo de disponibilidad  
  
> [!NOTE]  
>  Para ver la sintaxis y un ejemplo de un cmdlet dado, use la `Get-Help` cmdlet en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] entorno de PowerShell. Para más información, consulte [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md).  
  
1.  Cambie el directorio (`cd`) a la instancia del servidor que va a hospedar la réplica principal.  
  
2.  Cree un objeto de réplica de disponibilidad en memoria para la réplica principal.  
  
3.  Cree un objeto de réplica de disponibilidad en memoria para cada réplica secundaria.  
  
4.  Cree el grupo de disponibilidad.  
  
    > [!NOTE]  
    >  La longitud máxima del nombre de un grupo de disponibilidad es 128 caracteres.  
  
5.  Una la nueva réplica secundaria al grupo de disponibilidad. Para obtener más información, vea [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
6.  Para cada base de datos del grupo de disponibilidad, cree una base de datos secundaria restaurando las copias de seguridad recientes de la base de datos principal, utilizando RESTORE WITH NORECOVERY.  
  
7.  Una cada nueva base de datos secundaria al grupo de disponibilidad. Para obtener más información, vea [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md).  
  
8.  También puede utilizar las ventanas de `dir` comando para comprobar el contenido del nuevo grupo de disponibilidad.  
  
> [!NOTE]  
>  Si las cuentas de servicio de las instancias del servidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecutan en usuarios de dominio diferentes, cree en cada instancia del servidor un inicio de sesión para la otra instancia del servidor y conceda el permiso CONNECT de inicio de sesión para tener acceso al extremo de creación de reflejo de la base de datos local.  
  
##  <a name="ExampleConfigureGroup"></a> Ejemplo: Usar PowerShell para crear un grupo de disponibilidad  
 En el siguiente ejemplo de PowerShell se crea y configura un grupo de disponibilidad simple denominado `MyAG` con dos réplicas de disponibilidad y una base de datos de disponibilidad. El ejemplo:  
  
1.  Hace una copia de seguridad de `MyDatabase` y su registro de transacciones.  
  
2.  Restaura `MyDatabase` y su transacción inicie, usando la `-NoRecovery` opción.  
  
3.  Crea una representación de memoria de la réplica principal, que se hospedará en la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominada `PrimaryComputer\Instance`).  
  
4.  Crea una representación de memoria de la réplica secundaria, que se hospedará en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (denominada `SecondaryComputer\Instance`).  
  
5.  Crea un grupo de disponibilidad denominado `MyAG`.  
  
6.  Combina la réplica secundaria con el grupo de disponibilidad.  
  
7.  Combina la base de datos secundaria con el grupo de disponibilidad.  
  
```  
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "MyDatabase" `  
    -BackupFile "\\share\backups\MyDatabase.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "MyAG" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "MyDatabase"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "MyAG"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\MyAG" -Database "MyDatabase"  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar una instancia del servidor para grupos de disponibilidad AlwaysOn**  
  
-   [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
-   [Crear una base de datos de extremo de reflejo para grupos de disponibilidad AlwaysOn &#40;PowerShell de SQL Server&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
 **Para configurar el grupo de disponibilidad y las propiedades de réplica**  
  
-   [Cambiar el modo de disponibilidad de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
-   [Cambiar el modo de conmutación por error de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Configurar la directiva de conmutación por error Flexible para controlar las condiciones para la conmutación automática por error (grupos de disponibilidad AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
-   [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
-   [Configurar el acceso de solo lectura en una réplica de disponibilidad &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [Cambiar el tiempo de espera de la sesión en una réplica de disponibilidad &#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **Para completar la configuración del grupo de disponibilidad**  
  
-   [Combinar una réplica secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **Maneras alternativas de crear un grupo de disponibilidad**  
  
-   [Usar el Asistente para grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Crear un grupo de disponibilidad &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md)  
  
 **Para solucionar problemas de configuración de grupos de disponibilidad AlwaysOn**  
  
-   [Solucionar problemas de grupos de configuración de disponibilidad AlwaysOn (SQL Server) eliminado](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [Solucionar problemas de una operación de agregar archivos con error &#40;grupos de disponibilidad AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   **Blogs:**  
  
     [AlwaysON - HADRON Learning Series: Worker Pool Usage for HADRON Enabled bases de datos](http://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [Configurar AlwaysOn con SQL Server PowerShell](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/03/configuring-alwayson-with-sql-server-powershell.aspx)  
  
     [Blogs del equipo de AlwaysOn SQL Server: El Blog oficial del SQL Server AlwaysOn equipo](http://blogs.msdn.com/b/sqlalwayson/)  
  
     [Blogs de los ingenieros de SQL Server de CSS](http://blogs.msdn.com/b/psssql/)  
  
-   **Vídeos:**  
  
     [Microsoft SQL Server Code-Named "Denali", serie AlwaysOn, parte 1: Introducción a la solución de alta disponibilidad de siguiente generación](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server Code-Named "Denali", serie AlwaysOn, parte 2: Crear una solución esencial de alta disponibilidad utilizando AlwaysOn](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **Notas del producto:**  
  
     [Guía de soluciones de Microsoft SQL Server AlwaysOn para alta disponibilidad y recuperación ante desastres](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [Notas del producto de Microsoft para SQL Server 2012](http://msdn.microsoft.com/library/hh403491.aspx)  
  
     [Notas del producto del equipo de asesoramiento al cliente de SQL Server](http://sqlcat.com/)  
  
## <a name="see-also"></a>Vea también  
 [El punto de conexión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  