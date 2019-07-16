---
title: Realizar un seguimiento de las alertas del dispositivo - Analytics Platform System | Microsoft Docs
description: Realizar un seguimiento de las alertas del dispositivo en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 62f116b8e45512d5a6fc5ce50c0fbc76344103be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960028"
---
# <a name="track-appliance-alerts-in-analytics-platform-system"></a>Realizar un seguimiento de las alertas del dispositivo en Analytics Platform System
En este tema se explica cómo usar la consola de administración y las vistas del sistema para realizar un seguimiento de las alertas en un dispositivo PDW de SQL Server.  
  
## <a name="to-track-appliance-alerts"></a>Para realizar el seguimiento de las alertas del dispositivo  
PDW de SQL Server crea alertas para los problemas de hardware y software que requieren atención. Cada alerta contiene un título y una descripción del problema.  
  
PDW de SQL Server registra las alertas en el [sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV. El sistema conserva un límite de 10 000 alertas y elimina la alerta más antigua en primer lugar cuando se supera el límite.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>Ver alertas mediante el uso de la consola de administración  
Hay un **alertas** ficha para la región PDW y para la región de tejido del dispositivo. Después de producirse la conmutación por error, el evento de conmutación por error se incluye en el número de alertas en la página. Hay una página de la región PDW y la región de tejido del dispositivo. Cada página de mantenimiento tiene una pestaña. Para obtener más información sobre una alerta, haga clic en el **mantenimiento** página, el **alertas** pestaña y, a continuación, haga clic en una alerta.  
  
![Alertas de consola de administración PDW](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
En el **alertas** página:  
  
-   Para ver el historial de la alerta, haga clic en el **historial de alertas de revisión** vínculo.  
  
-   Para ver la alerta de componente y sus valores de propiedad actuales, haga clic en la fila de la alerta.  
  
-   Para ver detalles sobre el nodo que provocó la alerta, haga clic en el nombre del nodo.  
  
### <a name="view-alerts-by-using-the-system-views"></a>Ver alertas mediante el uso de las vistas del sistema  
Para ver las alertas mediante el uso de vistas del sistema, consulte [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md). Esta DMV muestra las alertas que no se han corregido. Para obtener ayuda con la selección de las alertas y errores, use el [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV.  
  
El ejemplo siguiente es una consulta común para ver las alertas actuales.  
  
```sql  
SELECT   
    aa.[pdw_node_id],  
    n.[name] AS [node_name],  
    g.[group_name] ,  
    c.[component_name] ,  
    aa.[component_instance_id] ,   
    a.[alert_name] ,  
    a.[state] ,  
    a.[severity] ,  
    aa.[current_value] ,  
    aa.[previous_value] ,  
    aa.[create_time] ,  
    a.[description]   
FROM [sys].[dm_pdw_component_health_active_alerts] AS aa  
    INNER JOIN sys.dm_pdw_nodes AS n   
        ON aa.[pdw_node_id] = n.[pdw_node_id]  
    INNER JOIN [sys].[pdw_health_components] AS c   
        ON aa.[component_id] = c.[component_id]  
    INNER JOIN [sys].[pdw_health_component_groups] AS g   
        ON c.[group_id] = g.[group_id]  
    INNER JOIN [sys].[pdw_health_alerts] AS a   
        ON aa.[alert_id] = a.[alert_id] and aa.[component_id] = c.[component_id]  
ORDER BY  
    a.alert_id ,  
    aa.[pdw_node_id];  
```  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->
[Supervisión del dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
