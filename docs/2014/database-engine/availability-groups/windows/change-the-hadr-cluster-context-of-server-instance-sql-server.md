---
title: Cambiar el contexto de clúster de HADR de la instancia de servidor (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- Availability replicas [SQL Server], change WSFC cluster context
ms.assetid: ecd99f91-b9a2-4737-994e-507065a12f80
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: de783ffdb5480a9cdebec2380f81e50a9cba11ec
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53361357"
---
# <a name="change-the-hadr-cluster-context-of-server-instance-sql-server"></a>Cambiar el contexto de clúster de HADR de la instancia de servidor (SQL Server)
  En este tema se describe cómo cambiar el contexto de clúster de HADR de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] en [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] y versiones posteriores. El *contexto de clúster de HADR* determina qué clúster de Clústeres de conmutación por error de Windows Server (WSFC) administra los metadatos para las réplicas de disponibilidad hospedadas por la instancia de servidor.  
  
 Cambie el contexto de clúster de HADR solo durante una migración entre clústeres de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] a una instancia de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] en un nuevo clúster de WSFC. La migración entre clústeres de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] admite la actualización del sistema operativo a [!INCLUDE[win8](../../../includes/win8-md.md)] o [!INCLUDE[win8srv](../../../includes/win8srv-md.md)] con un tiempo de inactividad mínimo de los grupos de disponibilidad. Para obtener más información, vea [Migración entre clústeres de grupos de disponibilidad AlwaysOn para la actualización del sistema operativo](https://msdn.microsoft.com/library/jj873730.aspx).  
  

  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
> [!CAUTION]  
>  Cambie el contexto de clúster de HADR solo durante la migración entre clústeres de implementaciones [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Solo puede cambiar el contexto de clúster de HADR desde el clúster local de WSFC a un clúster remoto y viceversa. No puede cambiar el contexto de clúster de HADR desde un clúster remoto a otro clúster remoto.  
  
-   El contexto de clúster de HADR se puede cambiar a un clúster remoto solo cuando la instancia de SQL Server no hospeda ninguna réplica de disponibilidad.  
  
-   Un contexto de clúster de HADR remoto se puede volver a cambiar al clúster local en cualquier momento. Sin embargo, el contexto no se puede cambiar de nuevo si la instancia de servidor hospeda réplicas de disponibilidad.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   La instancia de servidor en la que se cambia el contexto de clúster de HADR debe ejecutar [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] o superior (edición Enterprise o superior).  
  
-   La instancia de servidor debe estar habilitada para AlwaysOn. Para obtener más información, vea [Habilitar y deshabilitar grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   Para que se pueda cambiar de contexto de clúster local a un clúster remoto, una instancia de servidor no puede hospedar ninguna réplica de disponibilidad. La vista de catálogo [sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) no debe devolver ninguna fila.  
  
     Si existe alguna réplica de disponibilidad en la instancia de servidor, antes de poder cambiar el contexto de clúster de HADR debe hacer lo siguiente:  
  
    |Rol de réplica|Acción|Vínculo|  
    |------------------|------------|----------|  
    |Principal|Deja sin conexión el grupo de disponibilidad.|[Poner sin conexión un grupo de disponibilidad &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)|  
    |Secundario|Quitar la réplica de su grupo de disponibilidad|[Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)|  
  
-   Antes de poder cambiar de un clúster remoto al clúster local, todas las réplicas con confirmación sincrónica deben estar en el estado SYNCHRONIZED.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Se recomienda especificar el nombre de dominio completo. Esto es porque para buscar la dirección IP de destino de un nombre corto, ALTER SERVER CONFIGURATION usa la resolución de DNS. En algunas situaciones, en función del orden de búsqueda de DNS, el uso de un nombre corto puede producir confusiones. Por ejemplo, considere el comando siguiente, que se ejecuta en un nodo del dominio `abc` (`node1.abc.com`). El clúster de destino previsto es el clúster `CLUS01` del dominio `xyz` (`clus01.xyz.com`). Sin embargo, el dominio local hospeda también un clúster denominado `CLUS01` (`clus01.abc.com`).  
  
     Si se especificara el nombre corto del clúster de destino, `CLUS01`, la resolución de nombres DNS podría devolver la dirección IP del clúster erróneo, `clus01.abc.com`. Para evitar esa confusión, especifique el nombre completo del clúster de destino, como en el ejemplo siguiente:  
  
    ```  
    ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com'  
    ```  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
  
-   **inicio de sesión de SQL Server**  
  
     Requiere el permiso CONTROL SERVER.  
  
-   **Cuenta de servicio de SQL Server**  
  
     La cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de la instancia de servidor debe tener:  
  
    -   Permiso para abrir el clúster de destino de WSFC.  
  
    -   Acceso remoto de lectura y escritura de WSFC.  
  
 
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para cambiar el contexto de clúster de WSFC de una réplica de disponibilidad**  
  
1.  Conéctese a la instancia de servidor que hospeda la réplica principal o una réplica secundaria del grupo de disponibilidad.  
  
2.  Use la cláusula SET HADR CLUSTER CONTEXT de la instrucción [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql) , de la manera siguiente:  
  
     ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT **=** { **'*`windows_cluster`*'** | LOCAL}  
  
     donde,  
  
     *windows_cluster*  
     Nombre de objeto de clúster (CON) de un clúster de WSFC. Puede especificar el nombre corto o el nombre de dominio completo. Se recomienda especificar el nombre de dominio completo. Para obtener más información, vea [Recomendaciones](#Recommendations), anteriormente en este tema.  
  
     LOCAL  
     Clúster local de WSFC.  
  
### <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el contexto de clúster de HADR otro clúster diferente. Para identificar el clúster de destino de WSFC, `clus01`, el ejemplo especifica el nombre de objeto completo del clúster, `clus01.xyz.com`.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
 En el ejemplo siguiente se cambia el contexto de clúster de HADR al clúster local de WSFC.  
  
```  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = LOCAL;  
```  
  

  
##  <a name="FollowUp"></a> Sigue: Después de cambiar el contexto de clúster de una réplica de disponibilidad  
 El nuevo contexto de clúster de HADR surte efecto inmediatamente, sin necesidad de reiniciar la instancia de servidor. El valor de contexto del clúster de HADR es una configuración persistente de nivel de instancia que permanece sin modificar si se reinicia la instancia de servidor.  
  
 Confirme el nuevo contexto de clúster de HADR consultando la vista de administración dinámica [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql) , de la manera siguiente:  
  
```  
SELECT cluster_name FROM sys.dm_hadr_cluster  
```  
  
 Esta consulta debe devolver el nombre del clúster al que se establece el contexto de clúster de HADR.  
  
 Cuando el contexto de clúster de HADR se cambia a un nuevo clúster:  
  
-   Los metadatos se limpian para quitar cualquier réplicas de disponibilidad que están hospedadas actualmente en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Todas las bases de datos que pertenecieron previamente a una réplica de disponibilidad están ahora en el estado RESTORING.  
  
 
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Quitar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](remove-an-availability-group-listener-sql-server.md)  
  
-   [Poner sin conexión un grupo de disponibilidad &#40;SQL Server&#41;](../../take-an-availability-group-offline-sql-server.md)  
  
-   [Agregar una réplica secundaria a un grupo de disponibilidad &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [Quitar una réplica secundaria de un grupo de disponibilidad &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)  
  
-   [Crear o configurar un agente de escucha de grupo de disponibilidad &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
 
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Artículos técnicos de SQL Server 2012](https://msdn.microsoft.com/library/bb418445\(SQL.10\).aspx)  
  
-   [Blog del equipo de AlwaysOn SQL Server: El blog del equipo de AlwaysOn oficial SQL Server](https://blogs.msdn.com/b/sqlalwayson/)  
  
  
  
## <a name="see-also"></a>Vea también  
 [Grupos de disponibilidad AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md) [agrupación en clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
