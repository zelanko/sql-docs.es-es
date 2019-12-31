---
title: Supervisar el estado del dispositivo
description: Cómo supervisar el estado de un dispositivo de sistema de plataforma de análisis mediante la consola de administración o mediante la consulta directa de las vistas de administración dinámica de almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b99123f81fcdddd74dc72d485d97e428ca59ed84
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400991"
---
# <a name="monitor-appliance-health-state"></a>Supervisar el estado de mantenimiento del dispositivo
En este artículo se explica cómo supervisar el estado de un dispositivo de sistema de plataforma de análisis mediante la consola de administración de o mediante la consulta directa de las vistas de administración dinámica de almacenamiento de datos paralelos. 
  
## <a name="to-monitor-the-appliance-state"></a>Para supervisar el estado del dispositivo  
Un administrador del sistema puede usar la consola de administración de o las PDW de SQL Server vistas de administración dinámica (DMV) para recuperar la jerarquía completa de nodos, componentes y software. En el siguiente diagrama se ofrece una descripción de alto nivel de los componentes que PDW de SQL Server supervisa.  
  
![Información general de la supervisión](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Supervisar el estado de los componentes mediante la consola de administración  
Para recuperar el estado de los componentes mediante la consola de administración:  
  
1.  Haga clic en la pestaña **Estado del dispositivo** .  
  
2.  En la página estado del dispositivo, haga clic en un nodo específico para ver los detalles del nodo.  
  
    ![Estado de la consola de administración de PDW](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>Supervisar el estado de los componentes mediante las vistas del sistema  
Para recuperar el estado de los componentes mediante las vistas del sistema, utilice [Sys. dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md). Por ejemplo, la consulta siguiente recupera el estado de todos los componentes.  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
Los valores posibles devueltos para la propiedad status son:  
  
-   Aceptar  
  
-   No crítico  
  
-   Crítico  
  
-   Desconocido  
  
-   No compatible  
  
-   No accesible  
  
-   irrecuperable  
  
Para ver todas las propiedades de todos los componentes, quite `WHERE  p.property_name = 'Status'` la cláusula.  
  
La columna **[Update_time]** muestra la última vez que los agentes de mantenimiento de PDW de SQL Server sondean el componente.  
  
> [!CAUTION]  
> Asegúrese de investigar el problema cuando un componente no se ha sondeado durante 5 minutos o más. podría haber una alerta que indique un problema con los latidos de software.  
  
## <a name="see-also"></a>Véase también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión de dispositivos &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
