---
title: Realizar un seguimiento de las alertas de dispositivo (Analytics Platform System)
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
ms.assetid: 631345d9-4967-461a-8922-e5f8fd33f48f
caps.latest.revision: "14"
ms.openlocfilehash: a3ceaf032eed1af4ac6caeb6deb317a6eb54cc8d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="track-appliance-alerts"></a>Realizar un seguimiento de las alertas de dispositivo
Este tema explica cómo usar la consola de administración y las vistas del sistema para realizar un seguimiento de las alertas en un dispositivo PDW de SQL Server.  
  
## <a name="to-track-appliance-alerts"></a>Para realizar el seguimiento de las alertas de dispositivo  
SQL Server PDW crea alertas para los problemas de hardware y software que necesitan atención. Cada alerta contiene un título y una descripción del problema.  
  
SQL Server PDW registra las alertas en el [sys.dm_pdw_component_health_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-alerts-transact-sql.md) DMV. El sistema conserva un límite de 10.000 alertas y elimina la alerta más antigua en primer lugar cuando se supera el límite.  
  
### <a name="view-alerts-by-using-the-admin-console"></a>Ver alertas mediante la consola de administración  
Hay un **alertas** pestaña de la región PDW, la región HDI y para la región de tejido de la aplicación. Después de producirse la conmutación por error, el evento de conmutación por error se incluye en el número de alertas en la página. Hay una página de la región PDW, la región HDI y para la región de tejido de la aplicación. Cada página de mantenimiento tiene una pestaña. Para obtener más información sobre una alerta, haga clic en el **estado** página, el **alertas** ficha y, a continuación, haga clic en una alerta.  
  
![Las alertas de la consola de administración PDW](./media/track-appliance-alerts/SQL_Server_PDW_AdminConsole_AlertsV2.png "SQL_Server_PDW_AdminConsole_AlertsV2")  
  
En el **alertas** página:  
  
-   Para ver el historial de alertas, haga clic en el **historial de alertas de revisión** vínculo.  
  
-   Para ver el componente de alerta y sus valores de propiedad actuales, haga clic en la fila de la alerta.  
  
-   Para ver detalles acerca del nodo que generó la alerta, haga clic en el nombre del nodo.  
  
### <a name="view-alerts-by-using-the-system-views"></a>Ver alertas mediante el uso de las vistas del sistema  
Para ver las alertas mediante el uso de vistas del sistema, consulte [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md). Esta DMV muestra alertas que no se han corregido. Para obtener ayuda con errores y evaluar las alertas, utilice la [sys.dm_pdw_errors](../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md) DMV.  
  
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
[Supervisión de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-monitoring.md)  
  
