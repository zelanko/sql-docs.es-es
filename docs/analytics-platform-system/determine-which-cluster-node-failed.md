---
title: Determinar qué nodo de clúster no pudo (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e001117-a1b6-4357-bf25-e85aba3f1cf0
caps.latest.revision: 21
ms.openlocfilehash: 201d11f7c3e5e7d50e1138ab41edf4fbdb60a6b9
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="determine-which-cluster-node-failed"></a>Determinar en qué nodo de clúster no se pudo
En este tema se describe cómo determinar el nombre del nodo PDW de SQL Server que se produjo un error después de que se ha producido un clúster de conmutación por error y se ha producido una alerta de conmutación por error de clúster. Como parte de la solución de problemas de un clúster de conmutación por error, debe determinar el nombre del nodo que generó un error antes de ponerse en contacto con Microsoft para ayudarle a resolver el problema.  
  
## <a name="Background"></a>Segundo plano  
Para lograr alta disponibilidad en SQL Server PDW, el nodo de Control y los nodos de cálculo se configuran como componentes activos o pasivos de clústeres de conmutación por error de Windows. Cuando se produce un error en un servidor activo responder a las solicitudes de críticos del sistema, el servidor pasivo conmuta por error y realiza las funciones del servidor que no se pudo.  
  
Después de un clúster de conmutación por error, cuando SQL Server PDW informa sobre el estado de nodo, el servidor pasivo tiene un error sobre el estado. Sin embargo, no resulta evidente qué nodo o el servidor no se pudo, especialmente si el servidor que no se pudo sigue estando en línea. Para solucionar el error de clúster, debe determinar el nombre del nodo que conmutar por error.  
  
## <a name="AdminConsoleSolution"></a>Solución de la consola de administración  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Para buscar el nombre del nodo que no se pudo  
  
1.  Abra la consola de administración. Para obtener más información acerca de la consola de administración, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). Después de producirse la conmutación por error, el evento de conmutación por error se incluye en el número de alertas en el **estado** página. Hay un **estado** página de la región PDW, la región HDI y para la región de tejido de la aplicación. Cada página de estado tiene un **alertas** ficha. Para obtener más información sobre una alerta, haga clic en la página de mantenimiento, la ficha alertas y, a continuación, haga clic en una alerta.  
  
## <a name="SystemView"></a>Solución de vista del sistema  
La siguiente instrucción SQL muestra cómo utilizar el [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) vista del sistema para buscar el nombre del servidor que no se pudo.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
