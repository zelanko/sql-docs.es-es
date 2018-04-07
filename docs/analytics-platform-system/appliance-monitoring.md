---
title: Aplicación de supervisión (Analytics Platform System)
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
ms.assetid: 253864fb-9178-41d2-a0ae-5dd9fd0a4fda
caps.latest.revision: 25
ms.openlocfilehash: f361b56581fd5a8dadb4ff41c387074abc006879
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="appliance-monitoring"></a>Supervisión de dispositivo
Esta guía de supervisión de dispositivo describe las herramientas y tareas para supervisar el dispositivo PDW de SQL Server.  
  
## <a name="Basics"></a>Aspectos básicos de supervisión y herramientas  
Los valores y la información que se puede supervisar en el dispositivo PDW de SQL Server son amplias. Por ejemplo, los siguientes son típicos de tareas de supervisión.  
  
-   Busque las alertas emitidas por PDW de SQL Server.  
  
-   Monitor de hardware con errores.  
  
-   Supervisión de problemas de conectividad de red.  
  
-   Busque los errores devueltos a los usuarios durante el procesamiento de consultas.  
  
-   Ver el número de sesiones actualmente activas y las consultas.  
  
-   Compruebe el estado de carga, las copias de seguridad y restauraciones.  
  
### <a name="appliance-monitoring-tools"></a>Herramientas de supervisión de dispositivo  
Hay varias herramientas disponibles para supervisar el dispositivo.  
  
Consola de administración  
PDW de SQL Server tiene una consola de administración. Se trata de una herramienta basada en web que muestra información acerca de las consultas, carga, copia de seguridad y restauración, bloqueos, sesiones, alertas y estado de dispositivo. La consola de administración se ejecuta en el dispositivo. los usuarios conectarse a la consola de administración a través de Internet Explorer. Para obtener más información, vea:  
  
-   [Supervisar el dispositivo mediante la consola de administración &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![Las alertas de la consola de administración PDW](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Vistas del sistema  
PDW de SQL Server incluye vistas del sistema completa que le permiten obtener información detallada sobre el estado de dispositivo, el estado y el rendimiento. Para obtener una lista de vistas del sistema para tareas de supervisión, consulte:  
  
-   [Supervisar el dispositivo mediante el uso de vistas del sistema &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
PDW de SQL Server tiene una amplia integración con Systems Center Operations Manager. Los módulos de administración para SQL Server PDW están disponibles como descarga gratuita. Para obtener más información acerca del uso de System Center para supervisar SQL Server PDW, vea lo siguiente:  
  
-   [Supervisar el dispositivo mediante el uso de System Center Operations Manager &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluciones personalizadas  
En situaciones cuando System Center no está disponible con el centro de datos, herramientas de supervisión puede supervisar el equipo mediante el uso de una solución de supervisión de aplicaciones de terceros. Instalación de agentes de software externo actualmente no se admite en PDW, pero la mayoría de soluciones de supervisión admite Transact\-integración de SQL, por lo que el administrador del sistema puede implementar Transact directa\-consultas SQL en su PDW dispositivo.  
  
Si la solución de supervisión no admite directa Transact\-consultas SQL, o si no tiene una herramienta de supervisión, a continuación, puede utilizar scripts para realizar tareas de supervisión, como el envío de correo electrónico cuando se produzca una alerta.  El sitio wiki de TechNet contiene un ejemplo de solución de supervisión con scripts.  
  
-   [Ejemplo de supervisión para SQL Server PDW de Power Shell](http://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Relacionados con tareas de supervisión  
  
|Tarea de supervisión|Description|  
|-------------------|---------------|  
|Supervisar el dispositivo mediante la consola de administración.|[Supervisar el dispositivo mediante la consola de administración &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Supervisar el equipo mediante el uso de vistas del sistema.|[Supervisar el dispositivo mediante el uso de vistas del sistema &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Supervisar el dispositivo mediante el uso de System Center|[Supervisar el dispositivo mediante el uso de System Center Operations Manager &#40;sistema de la plataforma de análisis&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Supervisar el estado del dispositivo.|[Monitor de estado de dispositivo &#40;sistema de la plataforma de análisis&#41;](monitor-appliance-health-state.md)|  
|La supervisión de latidos.|[Enviar comentarios de telemetría a Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Realizar un seguimiento de las alertas de dispositivo.|[Realizar un seguimiento de las alertas de dispositivo &#40;sistema de la plataforma de análisis&#41;](track-appliance-alerts.md)|  
|Determine cuánta capacidad se está usando.|[Utilización de la capacidad de ver &#40;sistema de la plataforma de análisis&#41;](view-capacity-utilization.md)|  
|Determinar la frecuencia de sondeo del dispositivo.|[Determinar la frecuencia de sondeo &#40;sistema de la plataforma de análisis&#41;](determine-polling-frequency.md)|  
|Cuando se produce un error de clúster, determinar qué clúster de nodo de error.|[Determinar en qué nodo de clúster no se pudo &#40;sistema de la plataforma de análisis&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Tareas de administración de dispositivo &#40;sistema de la plataforma de análisis&#41;](appliance-management-tasks.md)  
  
