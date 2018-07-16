---
title: Ver las propiedades del grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server]
ms.assetid: 61243c87-bd62-4510-863f-2a8f347caf1f
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7c59f778735c524ca8b1d0b41469114b21e5b591
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312325"
---
# <a name="view-availability-group-properties-sql-server"></a>Ver las propiedades del grupo de disponibilidad (SQL Server)
  En este tema se describe cómo pueden verse las propiedades de un grupo disponibilidad AlwaysOn con [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  

  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para ver y cambiar las propiedades de un grupo de disponibilidad**  
  
1.  En el Explorador de objetos, conéctese a la instancia del servidor que hospeda la réplica principal y expanda el árbol.  
  
2.  Expanda los nodos **Alta disponibilidad de AlwaysOn** y **Grupos de disponibilidad** .  
  
3.  Haga clic con el botón secundario en el grupo de disponibilidad cuyas propiedades desea ver y seleccione el comando **Propiedades** .  
  
4.  En el cuadro de diálogo **Propiedades de grupo de disponibilidad** , use las páginas **General** y **Preferencias de copia de seguridad** para ver y, en algunos casos, cambiar las propiedades del grupo de disponibilidad seleccionado. Para más información, vea [Propiedades de grupo de disponibilidad y nuevo grupo de disponibilidad &#40;página General&#41;](availability-group-properties-new-availability-group-general-page.md) y [Propiedades de grupo de disponibilidad: Nuevo grupo de disponibilidad &#40;página Preferencias de copia de seguridad&#41;](availability-group-properties-new-availability-group-backup-preferences-page.md).  
  
     Use la página de **Permisos** para ver los inicios de sesión, roles y permisos explícitos actuales asociados al grupo de disponibilidad. Para más información, consulte [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md).  
  

  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver las propiedades y el estado de un grupo de disponibilidad**  
  
 Para consultar las propiedades y los estados de los grupos de disponibilidad en los que la instancia de servidor hospeda una réplica de disponibilidad, use las vistas siguientes:  
  
 [sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)  
 Devuelve una fila para cada grupo de disponibilidad para el que la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hospeda una réplica de disponibilidad. Cada fila contiene una copia almacenada en caché de los metadatos del grupo de disponibilidad.  
  
 **Nombres de columna:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference y automated_backup_preference_desc  
  
 [sys.availability_groups_cluster](/sql/relational-databases/system-catalog-views/sys-availability-groups-cluster-transact-sql)  
 Devuelve una fila para cada grupo de disponibilidad del clúster de WSFC. Cada fila contiene los metadatos del grupo de disponibilidad procedentes del clúster de clústeres de conmutación por error de Windows Server (WSFC).  
  
 **Nombres de columna:** group_id, name, resource_id, resource_group_id, failure_condition_level, health_check_timeout, automated_backup_preference y automated_backup_preference_desc  
  
 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql)  
 Devuelve una fila para cada grupo de disponibilidad que posee una réplica de disponibilidad en la instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cada fila muestra los estados que definen el estado de un grupo de disponibilidad determinado.  
  
 **Nombres de columna:** group_id, primary_replica, primary_recovery_health, primary_recovery_health_desc, secondary_recovery_health, secondary_recovery_health_desc, synchronization_health y synchronization_health_desc  
  

  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para obtener más información acerca de los grupos de disponibilidad**  
  
-   [Ver las propiedades de una réplica de disponibilidad &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Ver las propiedades del agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-listener-properties-sql-server.md)  
  
-   [Directivas de AlwaysOn para problemas operativos con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md)
  
-   [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](monitor-availability-groups-transact-sql.md)  
  
 **Para configurar un grupo de disponibilidad existente**  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Agregar una base de datos a un grupo de disponibilidad &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
-   [Quitar una base de datos secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
-   [Quitar una base de datos principal de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
-   [Quitar un grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)  
  
 **Para realizar la conmutación por error manual de un grupo de disponibilidad**  
  
-   [Realizar una conmutación por error manual planeada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Realizar una conmutación por error manual forzada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  

  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41; ](overview-of-always-on-availability-groups-sql-server.md) [supervisar grupos de disponibilidad &#40;Transact-SQL&#41; ](monitor-availability-groups-transact-sql.md) [directivas de AlwaysOn para problemas operativos con AlwaysOn Grupos de disponibilidad &#40;SQL Server&#41;](always-on-policies-for-operational-issues-always-on-availability.md) 
  
  
