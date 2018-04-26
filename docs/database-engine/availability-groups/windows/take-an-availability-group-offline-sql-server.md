---
title: Poner sin conexión un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: availability-groups
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], take offline
ms.assetid: 50f5aad8-0dff-45ef-8350-f9596d3db898
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 097d1c9a71939d9a28e578ef130a2a9b68dc310c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="take-an-availability-group-offline-sql-server"></a>Poner sin conexión un grupo de disponibilidad (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se explica cómo pasar un grupo de disponibilidad AlwaysOn del estado ONLINE el estado OFFLINE mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] en [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] y versiones posteriores. No se produce ninguna pérdida de datos en las bases de datos con confirmación sincrónica porque si alguna réplica con confirmación sincrónica no está sincronizada, la operación OFFLINE produce un error y deja el grupo de disponibilidad en el estado ONLINE. Mantener el grupo de disponibilidad en línea protege las bases de datos con confirmación sincrónica no sincronizadas frente a posibles pérdidas de datos. Cuando un grupo de disponibilidad pasa a estar sin conexión, sus bases de datos dejan de estar disponibles para los clientes y no puede volver a poner el grupo de disponibilidad en línea. Por tanto, ponga un grupo de disponibilidad sin conexión únicamente para migrar los recursos del grupo de disponibilidad de un clúster de WSFC a otro.  
  
 Si durante una migración entre clústeres de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]algunas aplicaciones se conectan directamente a la réplica principal de un grupo de disponibilidad, se debe poner sin conexión el grupo de disponibilidad. La migración entre clústeres de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] admite la actualización del sistema operativo con un tiempo de inactividad mínimo de los grupos de disponibilidad. El escenario habitual es usar la migración entre clústeres de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] para actualizar el sistema operativo a [!INCLUDE[win8](../../../includes/win8-md.md)] o a [!INCLUDE[win8srv](../../../includes/win8srv-md.md)]. Para obtener más información, vea [Migración entre clústeres de grupos de disponibilidad AlwaysOn para la actualización del sistema operativo](http://msdn.microsoft.com/library/jj873730.aspx).  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para poner un grupo de disponibilidad sin conexión, mediante:**  [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de que el grupo de disponibilidad esté sin conexión](#FollowUp)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
> [!CAUTION]  
>  Use la opción OFFLINE solo para realizar una migración entre clústeres de los recursos de un grupo de disponibilidad.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   La instancia de servidor en la que se escribe el comando OFFLINE debe ejecutar [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] o superior (edición Enterprise o superior).  
  
-   El grupo de disponibilidad debe estar actualmente en línea.  
  
###  <a name="Recommendations"></a> Recomendaciones  
 Antes de poner el grupo de disponibilidad sin conexión, elimine el agente o los agentes de escucha del grupo de disponibilidad. Para obtener más información, vea [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para poner sin conexión un grupo de disponibilidad**  
  
1.  Conéctese a una instancia de servidor que hospede una réplica de disponibilidad para el grupo de disponibilidad. Esta réplica puede ser la réplica principal o una réplica secundaria.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *group_name* OFFLINE  
  
     donde *group_name* es el nombre del grupo de disponibilidad.  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se pone sin conexión el grupo de disponibilidad `AccountsAG` .  
  
```  
ALTER AVAILABILITY GROUP AccountsAG OFFLINE;  
```  
  
##  <a name="FollowUp"></a> Seguimiento: después de que el grupo de disponibilidad esté sin conexión  
  
-   **Registro de la operación OFFLINE**  : La identidad del nodo de WSFC donde se inició la operación OFFLINE se almacena tanto en el registro de clúster de WSFC como en el registro de errores de SQL.  
  
-   **En el caso de que no se eliminara la escucha del grupo de disponibilidad antes de dejar a este último sin conexión:**  si va a migrar el grupo de disponibilidad a otro clúster WSFC, elimine el VNN y el VIP del agente de escucha. Puede eliminarlos mediante la consola Administración del clúster de conmutación por error, el cmdlet [Remove-ClusterResource](http://technet.microsoft.com/library/ee461015\(WS.10\).aspx) de PowerShell o [cluster.exe](http://technet.microsoft.com/library/ee461015\(WS.10\).aspx). Tenga en cuenta que cluster.exe está desusado en Windows 8.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Cambiar el contexto de clúster de HADR de la instancia de servidor &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Artículos técnicos de SQL Server 2012](http://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [Blog del equipo de AlwaysOn de SQL Server: blog oficial del equipo de AlwaysOn de SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Ver también  
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
