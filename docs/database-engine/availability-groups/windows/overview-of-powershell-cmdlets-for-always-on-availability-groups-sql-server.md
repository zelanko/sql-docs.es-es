---
title: Información general de los cmdlets de PowerShell para grupos de disponibilidad AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], PowerShell cmdlets
- Availability Groups [SQL Server], about
- PowerShell [SQL Server], cmdlets
ms.assetid: b3fef0d5-b6d7-4386-a0f0-d06c165ad4de
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f4491943f13e515bda4d46285b1a1e0dd52dfd9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597874"
---
# <a name="overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server"></a>Información general de los cmdlets de PowerShell para grupos de disponibilidad AlwaysOn (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PowerShell es un shell de línea de comandos basado en tareas y un lenguaje de scripting diseñado especialmente para la administración del sistema. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] proporciona un conjunto de cmdlets de PowerShell en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que le permiten implementar, administrar y supervisar grupos de disponibilidad, réplicas de disponibilidad y bases de datos de disponibilidad.  
  
> [!NOTE]  
>  Un cmdlet de PowerShell se puede completar correctamente iniciando una acción. Esto no indica que el trabajo previsto, como la conmutación por error de un grupo de disponibilidad se haya completado. Cuando se genera el script de una secuencia de acciones, puede que tenga que comprobar el estado de las acciones y esperar a que se completen.  
  
 En este tema se describen los cmdlets de los siguientes conjuntos de tareas:  
  
-   [Configurar una instancia de servidor para grupos de disponibilidad AlwaysOn](#ConfiguringServerInstance)  
  
-   [Realizar copias de seguridad y restaurar bases de datos y registros de transacciones](#BnRcmdlets)  
  
-   [Crear y administrar un grupo de disponibilidad](#DeployManageAGs)  
  
-   [Crear y administrar un agente de escucha de un grupo de disponibilidad](#AGlisteners)  
  
-   [Crear y administrar una réplica de disponibilidad](#DeployManageARs)  
  
-   [Agregar y administrar una base de datos de disponibilidad](#DeployManageDbs)  
  
-   [Supervisar el estado de grupos de disponibilidad](#MonitorTblshtAGs)  
  
> [!NOTE]  
>  Para obtener una lista de los temas de los Libros en pantalla de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] en los que se describe cómo usar cmdlets para realizar tareas de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] , vea la sección "Tareas relacionadas” de [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="ConfiguringServerInstance"></a> Configurar AlwaysOn una instancia del servidor para grupos de disponibilidad  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|
|[**Disable-SqlAlwaysOn**](/powershell/module/sqlserver/disable-sqlalwayson)|Deshabilita la característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en una instancia de servidor.|La instancia de servidor especificada por el parámetro **Path**, **InputObject**o **Name** . (Debe ser una edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que admita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]).|  
|[**Enable-SqlAlwaysOn**](/powershell/module/sqlserver/enable-sqlalwayson)|Habilita [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] en una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] que admite la característica [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Para obtener más información sobre la compatibilidad de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vea [Requisitos previos, restricciones y recomendaciones para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md).|Cualquier edición de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que admite [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].|  
|[**New-SqlHadrEndPoint**](/powershell/module/sqlserver/new-sqlhadrendpoint)|Crea un nuevo extremo de creación de reflejo de la base de datos en una instancia de servidor. Este extremo es necesario para el movimiento de datos entre las bases de datos principal y secundaria.|Cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|  
|[**Set-SqlHadrEndpoint**](/powershell/module/sqlserver/set-sqlhadrendpoint)|Cambia las propiedades de un extremo de creación de reflejo de la base de datos existente, como el nombre, el estado o las propiedades de autenticación.|Una instancia de servidor que admite [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y no tiene un extremo de creación de reflejo de la base de datos|  

  
##  <a name="BnRcmdlets"></a> Copia de seguridad y restauración de bases de datos y registros de transacciones  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|[**Backup-SqlDatabase**](/powershell/module/sqlserver/backup-sqldatabase)|Crea una copia de seguridad de datos o del registro.|Cualquier base de datos en línea (en el caso [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], una base de datos de la instancia del servidor que hospeda la réplica principal)|  
|[**Restore-SqlDatabase**](/powershell/module/sqlserver/restore-sqldatabase)|Restaura una copia de seguridad.|Cualquier instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (en el caso de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], una instancia de servidor que hospeda una réplica secundaria)<br /><br />

  >[!Important]
  >Al preparar una base de datos secundaria, debe usar el parámetro **-NoRecovery** en cada comando **Restore-SqlDatabase**. 
  
 Para obtener más información sobre cómo usar estos cmdlets para preparar una base de datos secundaria, vea [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
##  <a name="DeployManageAGs"></a> Crear y administrar un grupo de disponibilidad  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|[**New-SqlAvailabilityGroup**](/powershell/module/sqlserver/new-sqlavailabilitygroup)|Crea un nuevo grupo de disponibilidad.|Instancia del servidor para hospedar la réplica principal|  
|[**Remove-SqlAvailabilityGroup**](/powershell/module/sqlserver/remove-sqlavailabilitygroup)|Elimina un grupo de disponibilidad.|Instancia del servidor habilitada para HADR|  
|[**Set-SqlAvailabilityGroup**](/powershell/module/sqlserver/set-sqlavailabilitygroup)|Establece las propiedades de un grupo de disponibilidad; poner en línea o sin conexión un grupo de disponibilidad|Instancia del servidor que hospeda la réplica principal|  
|[**Switch-SqlAvailabilityGroup**](/powershell/module/sqlserver/switch-sqlavailabilitygroup)|Inicia una de las siguientes formas de conmutación por error<br /><br /> Una conmutación por error forzada de un grupo de disponibilidad (con posible pérdida de datos).<br /><br /> Una conmutación por error manual de un grupo de disponibilidad.|Instancia del servidor que hospeda la réplica secundaria de destino|  
  
##  <a name="AGlisteners"></a> Crear y administrar un agente de escucha del grupo de disponibilidad  
  
|Cmdlet|Descripción|Se admite en|  
|------------|-----------------|------------------|  
|[**New-SqlAvailabilityGroupListener**](/powershell/module/sqlserver/new-sqlavailabilitygrouplistener)|Crea un nuevo agente de escucha del grupo de disponibilidad y lo adjunta a un grupo de disponibilidad existente.|Instancia del servidor que hospeda la réplica principal|  
|[**Set-SqlAvailabilityGroupListener**](/powershell/module/sqlserver/set-sqlavailabilitygrouplistener)|Modifica la configuración del puerto en un agente de escucha del grupo de disponibilidad existente.|Instancia del servidor que hospeda la réplica principal|  
|[**Add-SqlAvailabilityGroupListenerStaticIp**](/powershell/module/sqlserver/add-sqlavailabilitygrouplistenerstaticip)|Agrega una dirección IP estática a una configuración de agente de escucha del grupo de disponibilidad existente. La dirección IP estática puede ser una dirección IPv4 con subred o una dirección IPv6.|Instancia del servidor que hospeda la réplica principal|  
  
##  <a name="DeployManageARs"></a> Crear y administrar una réplica de disponibilidad  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|[**New-SqlAvailabilityReplica**](/powershell/module/sqlserver/new-sqlavailabilityreplica)|Crea una nueva réplica de disponibilidad. Puede usar el parámetro **-AsTemplate** para crear un objeto de réplica de disponibilidad en memoria para cada nueva réplica de disponibilidad.|Instancia del servidor que hospeda la réplica principal|  
|[**Join-SqlAvailabilityGroup**](/powershell/module/sqlserver/join-sqlavailabilitygroup)|Combina una réplica secundaria con el grupo de disponibilidad.|Instancia del servidor que hospeda la réplica secundaria|  
|[**Remove-SqlAvailabilityReplica**](/powershell/module/sqlserver/remove-sqlavailabilityreplica)|Elimina una réplica de disponibilidad.|Instancia del servidor que hospeda la réplica principal|  
|[**Set-SqlAvailabilityReplica**](/powershell/module/sqlserver/set-sqlavailabilityreplica)|Establece las propiedades de una réplica de disponibilidad.|Instancia del servidor que hospeda la réplica principal|  
  
##  <a name="DeployManageDbs"></a> Agregar y administrar una base de datos de disponibilidad  
  
|Cmdlets|Descripción|Se admite en|  
|-------------|-----------------|------------------|  
|[**Add-SqlAvailabilityDatabase**](/powershell/module/sqlserver/add-sqlavailabilitydatabase)|En la réplica principal, agrega una base de datos a un grupo de disponibilidad.<br /><br /> En una réplica secundaria, une una base de datos secundaria a un grupo de disponibilidad.|Cualquier instancia del servidor que hospeda una réplica de disponibilidad (el comportamiento difiere entre las réplicas principal y secundaria)|  
|[**Remove-SqlAvailabilityDatabase**](/powershell/module/sqlserver/remove-sqlavailabilitydatabase)|En la réplica principal, quita del grupo de disponibilidad la base de datos.<br /><br /> En una réplica secundaria, quita la base de datos secundaria local de la réplica secundaria local.|Cualquier instancia del servidor que hospeda una réplica de disponibilidad (el comportamiento difiere entre las réplicas principal y secundaria)|  
|[**Resume-SqlAvailabilityDatabase**](/powershell/module/sqlserver/resume-sqlavailabilitydatabase)|Reanuda el movimiento de datos en una base de datos de disponibilidad suspendida.|La instancia de servidor en la que se ha suspendido la base de datos.|  
|[**Suspend-SqlAvailabilityDatabase**](/powershell/module/sqlserver/suspend-sqlavailabilitydatabase)|Suspende el movimiento de datos en una base de datos de disponibilidad.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.|  
  
##  <a name="MonitorTblshtAGs"></a> Monitoring Availability Group Health  
 Los cmdlets siguientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permiten supervisar el estado de un grupo de disponibilidad y sus réplicas y bases de datos.  
  
> [!IMPORTANT]  
>  Debe tener permisos CONNECT, VIEW SERVER STATE y VIEW ANY DEFINITION para ejecutar estos cmdlets.  
  
|Cmdlet|Descripción|Se admite en|  
|------------|-----------------|------------------|  
|[**Test-SqlAvailabilityGroup**](/powershell/module/sqlserver/test-sqlavailabilitygroup)|Evalúa el estado de un grupo de disponibilidad mediante la evaluación de las directivas de administración basada en directivas (PBM) de SQL Server.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.*|  
|[**Test-SqlAvailabilityReplica**](/powershell/module/sqlserver/test-sqlavailabilityreplica)|Evalúa el estado de las réplicas de disponibilidad mediante la evaluación de las directivas de administración basada en directivas (PBM) de SQL Server.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.*|  
|[**Test-SqlDatabaseReplicaState**](/powershell/module/sqlserver/test-sqldatabasereplicastate)|Evalúa el estado de una base de datos de disponibilidad en todas las réplicas de disponibilidad mediante la evaluación de directivas de administración basada en directivas (PBM) de SQL Server.|Cualquier instancia de servidor que hospeda una réplica de disponibilidad.*|  
  
 *Para ver información acerca de todas las réplicas de disponibilidad en un grupo de disponibilidad, use la instancia del servidor que hospeda la réplica principal.  
  
 Para obtener más información, vea [Usar directivas de AlwaysOn para ver el estado de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Obtener ayuda de SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  
  
  
