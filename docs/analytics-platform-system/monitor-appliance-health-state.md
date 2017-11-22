---
title: Estado de mantenimiento del dispositivo de monitor (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91132e3c-3137-4670-adaa-8a7b234fb8d2
caps.latest.revision: "12"
ms.openlocfilehash: dad3355061bafcbbfa3a34b21d2043b0411129ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-appliance-health-state"></a>Monitor de estado de dispositivo
En este tema se explica cómo supervisar el estado de un dispositivo PDW de SQL Server mediante la consola de administración, o consultando directamente las vistas de administración dinámica de SQL Server PDW.  
  
## <a name="to-monitor-the-appliance-state"></a>Para supervisar el estado de dispositivo  
Un administrador del sistema puede utilizar la consola de administración o las vistas de administración dinámica (DMV) de SQL Server PDW para recuperar la jerarquía completa de nodos, componentes y software. El siguiente diagrama ofrece una visión de alto nivel de los componentes que supervisa PDW de SQL Server.  
  
![Información general sobre supervisión](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Supervisar el estado de componente mediante el uso de la consola de administración  
Para recuperar el estado del componente mediante el uso de la consola de administración:  
  
1.  Haga clic en el **estado de dispositivo** ficha.  
  
2.  En la página de estado de dispositivo, haga clic en un nodo específico para ver los detalles del nodo.  
  
    ![Estado de consola de administración de PDW](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>Supervisar el estado de componente mediante el uso de vistas del sistema  
Para recuperar el estado del componente mediante el uso de vistas del sistema, use [sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md). Por ejemplo, la consulta siguiente recupera el estado de todos los componentes.  
  
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
  
Posibles valores devueltos para la propiedad de estado son:  
  
-   Vale  
  
-   No críticos  
  
-   Crítico  
  
-   Desconocido  
  
-   No compatible  
  
-   Inaccesible  
  
-   Irrecuperable  
  
Para ver todas las propiedades para todos los componentes, quite el `WHERE  p.property_name = 'Status'` cláusula.  
  
El **[update_time]** columna muestra la última vez que el componente se sondeó por los agentes de mantenimiento de SQL Server PDW.  
  
> [!CAUTION]  
> Asegúrese de investigar el problema cuando un componente no ha sido encuestado durante 5 minutos o más; podría haber una alerta que indica un problema con los latidos del software.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-monitoring.md)  
  
