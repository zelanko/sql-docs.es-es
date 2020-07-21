---
title: Determinar el nodo de clúster con errores
description: En este artículo se describe cómo determinar el nombre del nodo de Analytics Platform System (APS) que produjo un error después de que se ha producido una conmutación por error de clúster y se ha generado una alerta de conmutación por error de clúster. Como parte de la solución de problemas de una conmutación por error de clúster, debe determinar el nombre del nodo con errores antes de ponerse en contacto con Microsoft para ayudar a resolver el problema.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 68ebdb7f17ddee311644e11c48eaa4b586beac74
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401206"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>Determinar en qué nodo de clúster se produjo un error en Analytics Platform System
En este tema se describe cómo determinar el nombre del nodo del sistema de plataforma de análisis (APS) que produjo un error después de que se ha producido una conmutación por error de clúster y se ha generado una alerta de conmutación por error de clúster. Como parte de la solución de problemas de una conmutación por error de clúster, debe determinar el nombre del nodo con errores antes de ponerse en contacto con Microsoft para ayudar a resolver el problema.  
  
## <a name="background"></a><a name="Background"></a>Segundo plano  
Para lograr una alta disponibilidad en PDW de SQL Server, el nodo de control y los nodos de proceso se configuran como componentes activos o pasivos de los clústeres de conmutación por error de Windows. Cuando un servidor activo no responde a las solicitudes críticas del sistema, el servidor pasivo conmuta por error y realiza las funciones del servidor en el que se produjo el error.  
  
Después de una conmutación por error de clúster, cuando PDW de SQL Server informes sobre el estado del nodo, el servidor pasivo tiene un estado de error. Sin embargo, no es obvio en qué servidor o nodo se produjo un error, especialmente si el servidor en el que se produjo el error todavía está en línea. Para solucionar el error del clúster, debe determinar el nombre del nodo que conmute por error.  
  
## <a name="admin-console-solution"></a><a name="AdminConsoleSolution"></a>Solución de la consola de administración  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Para buscar el nombre del nodo en el que se produjo un error  
  
1.  Abra la consola de administración de. Para obtener más información sobre la consola de administración, consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). Una vez que se produce la conmutación por error, el evento de conmutación por error se incluye en el número de alertas de la página de **Estado** . Hay una página de **Estado** para la región de PDW y para la región de tejido del dispositivo. Cada página de Estado tiene una pestaña **alertas** . Para obtener más información acerca de una alerta, haga clic en la página Estado, en la ficha alertas y, a continuación, haga clic en una alerta.  
  
## <a name="system-view-solution"></a><a name="SystemView"></a>Solución de vista del sistema  
La siguiente instrucción SQL muestra cómo utilizar la vista del sistema [Sys. dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) para buscar el nombre del servidor en el que se produjo el error.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
