---
title: Supervisión del dispositivo
description: En esta guía de supervisión de dispositivos se describen las herramientas y las tareas para supervisar el dispositivo de sistema de plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401424"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Supervisión del dispositivo para el sistema de plataforma de análisis
En esta guía de supervisión de dispositivos se describen las herramientas y las tareas para supervisar el dispositivo de sistema de plataforma de análisis.  
  
## <a name="monitoring-basics-and-tools"></a><a name="Basics"></a>Aspectos básicos y herramientas de supervisión  
Los valores y la información que se pueden supervisar en el PDW de SQL Server dispositivo son extensos. Por ejemplo, las siguientes tareas de supervisión son típicas.  
  
-   Compruebe si hay alguna alerta emitida por PDW de SQL Server.  
  
-   Monitor para el hardware con errores.  
  
-   Supervise los problemas de conectividad de red.  
  
-   Compruebe si hay errores devueltos a los usuarios durante el procesamiento de la consulta.  
  
-   Ver el número de sesiones y consultas activas actualmente.  
  
-   Compruebe el estado de las cargas, copias de seguridad y restauraciones.  
  
### <a name="appliance-monitoring-tools"></a>Herramientas de supervisión de dispositivos  
Hay varias herramientas disponibles para supervisar el dispositivo.  
  
Consola de administración  
PDW de SQL Server tiene una consola de administración. Se trata de una herramienta basada en Web que muestra información acerca de las consultas, las cargas, las copias de seguridad y restauración, los bloqueos, las sesiones, las alertas y el estado del dispositivo. La consola de administración se ejecuta en el dispositivo. los usuarios se conectan a la consola de administración a través de Internet Explorer. Para obtener más información, consulte:  
  
-   [Supervise el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![Alertas de consola de administración de PDW](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Vistas del sistema  
PDW de SQL Server incluye vistas completas del sistema que le permiten obtener información detallada acerca del estado del dispositivo, el estado y el rendimiento. Para obtener una lista de las vistas del sistema para las tareas de supervisión, consulte:  
  
-   [Supervise el dispositivo mediante las vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
PDW de SQL Server tiene una amplia integración con Systems Center Operations Manager. Los módulos de administración para PDW de SQL Server están disponibles como descarga gratuita. Para obtener más información acerca del uso de System Center para supervisar PDW de SQL Server, consulte lo siguiente:  
  
-   [Supervise el dispositivo mediante System Center Operations Manager &#40;de sistema de plataforma de análisis&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluciones personalizadas  
En situaciones en las que System Center no está disponible con las herramientas de supervisión de centros de datos, puede supervisar el dispositivo mediante una solución de supervisión de terceros. La instalación de agentes de software externo no se admite actualmente en PDW, pero la mayoría de\-las soluciones de supervisión admiten la integración de Transact SQL\-, por lo que el administrador del sistema puede implementar consultas Transact SQL directas en el dispositivo PDW.  
  
Si la solución de supervisión no admite consultas directas\-de Transact SQL o no dispone de una herramienta de supervisión, puede usar scripts para realizar tareas de supervisión, como enviar correo electrónico cuando se produce una alerta.  El sitio wiki de TechNet contiene un ejemplo de solución de supervisión con scripts.  
  
-   [Ejemplo de supervisión de Power Shell para PDW de SQL Server](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="related-monitoring-tasks"></a><a name="Tasks"></a>Tareas de supervisión relacionadas  
  
|Tarea de supervisión|Descripción|  
|-------------------|---------------|  
|Supervise el dispositivo mediante la consola de administración.|[Supervise el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Supervise el dispositivo mediante las vistas del sistema.|[Supervise el dispositivo mediante las vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Supervisar el dispositivo mediante System Center|[Supervise el dispositivo mediante System Center Operations Manager &#40;de sistema de plataforma de análisis&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Supervise el estado del dispositivo.|[Supervise el estado de mantenimiento del dispositivo &#40;Analytics Platform System&#41;](monitor-appliance-health-state.md)|  
|Supervisión de latidos.|[Enviar comentarios de telemetría a Microsoft &#40;PDW de SQL Server&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Realizar un seguimiento de las alertas del dispositivo.|[Realice un seguimiento de las alertas del dispositivo &#40;Analytics Platform System&#41;](track-appliance-alerts.md)|  
|Determine cuánta capacidad se está usando.|[Visualización del uso de la capacidad &#40;Analytics Platform System&#41;](view-capacity-utilization.md)|  
|Determinar la frecuencia de sondeo del dispositivo.|[Determine la frecuencia de sondeo &#40;Analytics Platform System&#41;](determine-polling-frequency.md)|  
|Cuando se produce un error de clúster, determine en qué nodo del clúster se produjo un error.|[Determine en qué nodo del clúster se ha producido un error &#40;Analytics Platform System&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Consulte también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Tareas de administración de dispositivos &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
