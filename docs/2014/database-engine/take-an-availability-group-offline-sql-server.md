---
title: Poner sin conexión un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], take offline
ms.assetid: 50f5aad8-0dff-45ef-8350-f9596d3db898
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 28d8279226469b8d7a39c5cf6ec802a393337087
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371377"
---
# <a name="take-an-availability-group-offline-sql-server"></a>Poner sin conexión un grupo de disponibilidad (SQL Server)
  En este tema se describe cómo pasar un grupo de disponibilidad AlwaysOn del estado ONLINE el estado OFFLINE mediante [!INCLUDE[tsql](../includes/tsql-md.md)] en [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] y versiones posteriores. No se produce ninguna pérdida de datos en las bases de datos con confirmación sincrónica porque si alguna réplica con confirmación sincrónica no está sincronizada, la operación OFFLINE produce un error y deja el grupo de disponibilidad en el estado ONLINE. Mantener el grupo de disponibilidad en línea protege las bases de datos con confirmación sincrónica no sincronizadas frente a posibles pérdidas de datos. Cuando un grupo de disponibilidad pasa a estar sin conexión, sus bases de datos dejan de estar disponibles para los clientes y no puede volver a poner el grupo de disponibilidad en línea. Por tanto, ponga un grupo de disponibilidad sin conexión únicamente para migrar los recursos del grupo de disponibilidad de un clúster de WSFC a otro.  
  
 Si durante una migración entre clústeres de [!INCLUDE[ssHADR](../includes/sshadr-md.md)]algunas aplicaciones se conectan directamente a la réplica principal de un grupo de disponibilidad, se debe poner sin conexión el grupo de disponibilidad. La migración entre clústeres de [!INCLUDE[ssHADR](../includes/sshadr-md.md)] admite la actualización del sistema operativo con un tiempo de inactividad mínimo de los grupos de disponibilidad. El escenario habitual es usar la migración entre clústeres de [!INCLUDE[ssHADR](../includes/sshadr-md.md)] para actualizar el sistema operativo a [!INCLUDE[win8](../includes/win8-md.md)] o a [!INCLUDE[win8srv](../includes/win8srv-md.md)]. Para obtener más información, vea [Migración entre clústeres de grupos de disponibilidad AlwaysOn para la actualización del sistema operativo](https://msdn.microsoft.com/library/jj873730.aspx).  
  

  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
> [!CAUTION]  
>  Use la opción OFFLINE solo para realizar una migración entre clústeres de los recursos de un grupo de disponibilidad.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   La instancia de servidor en la que se escribe el comando OFFLINE debe ejecutar [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] o superior (edición Enterprise o superior).  
  
-   El grupo de disponibilidad debe estar actualmente en línea.  
  
###  <a name="Recommendations"></a> Recomendaciones  
 Antes de poner el grupo de disponibilidad sin conexión, elimine el agente o los agentes de escucha del grupo de disponibilidad. Para obtener más información, vea [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Se requiere el permiso ALTER AVAILABILITY GROUP en el grupo de disponibilidad, el permiso CONTROL AVAILABILITY GROUP, el permiso ALTER ANY AVAILABILITY GROUP o el permiso CONTROL SERVER.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para poner sin conexión un grupo de disponibilidad**  
  
1.  Conéctese a una instancia de servidor que hospede una réplica de disponibilidad para el grupo de disponibilidad. Esta réplica puede ser la réplica principal o una réplica secundaria.  
  
2.  Use la instrucción [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) del siguiente modo:  
  
     ALTER AVAILABILITY GROUP *group_name* OFFLINE  
  
     donde *group_name* es el nombre del grupo de disponibilidad.  
  
### <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se pone sin conexión el grupo de disponibilidad `AccountsAG` .  
  
```  
ALTER AVAILABILITY GROUP AccountsAG OFFLINE;  
```  
  
##  <a name="FollowUp"></a> Sigue: Después de que el grupo de disponibilidad esté sin conexión  
  
-   **Registro de la operación sin conexión:**  La identidad del nodo WSFC donde se inició la operación OFFLINE se almacena en el registro del clúster WSFC y SQL ERRORLOG.  
  
-   **Si no se eliminara la escucha del grupo de disponibilidad antes de desconectar el grupo:**  Si va a migrar el grupo de disponibilidad a otro clúster WSFC, elimine el VNN y el VIP del agente de escucha. Puede eliminarlos mediante la consola Administración del clúster de conmutación por error, el cmdlet [Remove-ClusterResource](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx) de PowerShell o [cluster.exe](https://technet.microsoft.com/library/ee461015\(WS.10\).aspx). Tenga en cuenta que cluster.exe está desusado en Windows 8.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Cambiar el contexto de clúster de HADR de la instancia de servidor &#40;SQL Server&#41;](availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Artículos técnicos de SQL Server 2012](https://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [Blog del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>Vea también  
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
