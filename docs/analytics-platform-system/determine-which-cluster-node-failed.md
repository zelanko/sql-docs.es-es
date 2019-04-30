---
title: 'Determinar el nodo de clúster con errores: Analytics Platform System | Microsoft Docs'
description: En este artículo se describe cómo determinar el nombre del nodo de Analytics Platform System (APS) que se produjo un error después de que se ha producido un clúster de conmutación por error y se ha generado una alerta de conmutación por error de clúster. Como parte de la solución de problemas de un clúster de conmutación por error, debe determinar el nombre del nodo con error antes de ponerse en contacto con Microsoft para ayudar a resolver el problema.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4fd739e55725a3138a22539ef837088f86c8d8b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283146"
---
# <a name="determine-which-cluster-node-failed-for-analytics-platform-system"></a>Determinar qué clúster de nodo no se pudo para Analytics Platform System
Este tema describe cómo determinar el nombre del nodo de Analytics Platform System (APS) que se produjo un error después de que se ha producido un clúster de conmutación por error y se ha generado una alerta de conmutación por error de clúster. Como parte de la solución de problemas de un clúster de conmutación por error, debe determinar el nombre del nodo con error antes de ponerse en contacto con Microsoft para ayudar a resolver el problema.  
  
## <a name="Background"></a>En segundo plano  
Para lograr alta disponibilidad en PDW de SQL Server, el nodo de Control y los nodos de proceso se configuran como activos o pasivos componentes de clústeres de conmutación por error de Windows. Cuando se produce un error en un servidor activo responder a las solicitudes del sistema críticos, el servidor pasivo conmuta por error y realiza las funciones del servidor que no se pudo.  
  
Después de un clúster de conmutación por error, cuando PDW de SQL Server informa sobre el estado de nodo, el servidor pasivo tiene un error a través de estado. Sin embargo, no resulta evidente qué servidor o el nodo no se pudo, especialmente si el servidor que no se pudo todavía está en línea. Para solucionar el error de clúster, debe determinar el nombre del nodo que conmutan por error.  
  
## <a name="AdminConsoleSolution"></a>Solución de la consola de administración  
  
#### <a name="to-find-the-name-of-the-node-that-failed"></a>Para buscar el nombre del nodo con error  
  
1.  Abra la consola de administración. Para obtener más información acerca de la consola de administración, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md). Después de producirse la conmutación por error, el evento de conmutación por error se incluye en el número de alertas en el **mantenimiento** página. Hay un **mantenimiento** página de la región PDW y la región de tejido del dispositivo. Cada página de mantenimiento tiene una **alertas** ficha. Para obtener más información sobre una alerta, haga clic en la página de estado, la pestaña alertas y, a continuación, haga clic en una alerta.  
  
## <a name="SystemView"></a>Solución de vista del sistema  
La siguiente instrucción SQL muestra cómo usar el [sys.dm_pdw_component_health_active_alerts](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-active-alerts-transact-sql.md) vista del sistema para buscar el nombre del servidor que no se pudo.  
  
```sql  
SELECT  
SUBSTRING( component_instance_id, 2, charindex(' ', component_instance_id, 1)-2) AS failed_node_name,  
create_time AS failover_time  
FROM sys.dm_pdw_component_health_active_alerts  
WHERE alert_id = 500139  
ORDER BY failed_node_name;  
```  
  
