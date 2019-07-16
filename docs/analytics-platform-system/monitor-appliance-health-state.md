---
title: Supervisar el estado del dispositivo - Analytics Platform System
description: Cómo supervisar el estado de un dispositivo de Analytics Platform System mediante el uso de la consola de administración o consultando directamente las vistas de administración dinámica de almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c69e46ad6a37a17a12c37f83625b5c7f6eaf8078
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960612"
---
# <a name="monitor-appliance-health-state"></a>Monitor de estado de dispositivo
En este artículo se explica cómo supervisar el estado de un dispositivo de Analytics Platform System mediante el uso de la consola de administración o consultando directamente las vistas de administración dinámica de almacenamiento de datos paralelos. 
  
## <a name="to-monitor-the-appliance-state"></a>Para supervisar el estado del dispositivo  
Un administrador del sistema puede utilizar la consola de administración o las vistas de administración dinámica (DMV) de SQL Server PDW para recuperar la jerarquía completa del software, los componentes y los nodos. El diagrama siguiente ofrece una visión de alto nivel de los componentes que supervisa PDW de SQL Server.  
  
![Información general sobre supervisión](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>Supervisar el estado de componente mediante el uso de la consola de administración  
Para recuperar el estado del componente mediante el uso de la consola de administración:  
  
1.  Haga clic en el **estado de dispositivo** ficha.  
  
2.  En la página de estado del dispositivo, haga clic en un nodo específico para ver los detalles del nodo.  
  
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
  
-   De acuerdo  
  
-   No crítico  
  
-   Crítico  
  
-   Desconocido  
  
-   No compatible  
  
-   Inaccesible  
  
-   Irrecuperable  
  
Para ver todas las propiedades de todos los componentes, quite el `WHERE  p.property_name = 'Status'` cláusula.  
  
El **[update_time]** columna muestra la última vez que el componente se sondeó por los agentes de mantenimiento de PDW de SQL Server.  
  
> [!CAUTION]  
> Asegúrese de investigar el problema cuando un componente no ha sido encuestado durante 5 minutos o más. podría haber una alerta que indica un problema con los latidos de software.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión del dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
