---
title: Supervisión del dispositivo - Analytics Platform System | Microsoft Docs
description: Esta guía de supervisión de dispositivo describe las herramientas y tareas para supervisar la aplicación Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 100a587814e62a6455d25e78a3defca973f39bf6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63276137"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Supervisión del dispositivo para Analytics Platform System
Esta guía de supervisión de dispositivo describe las herramientas y tareas para supervisar la aplicación Analytics Platform System.  
  
## <a name="Basics"></a>Aspectos básicos de supervisión y herramientas  
Los valores y la información que puede supervisarse en el dispositivo PDW de SQL Server son inmensas. Por ejemplo, los siguientes son típicos de tareas de supervisión.  
  
-   Busque cualquier alerta de PDW de SQL Server.  
  
-   Supervisión de hardware con errores.  
  
-   Supervisión de problemas de conectividad de red.  
  
-   Compruebe si hay errores devueltos a los usuarios durante el procesamiento de consultas.  
  
-   Ver el número de sesiones actualmente activas y las consultas.  
  
-   Compruebe el estado de carga, las copias de seguridad y restauraciones.  
  
### <a name="appliance-monitoring-tools"></a>Herramientas de supervisión del dispositivo  
Hay varias herramientas disponibles para supervisar el dispositivo.  
  
Consola de administración  
PDW de SQL Server tiene una consola de administración. Esto es una herramienta basada en web que muestra información acerca de las consultas, cargas, copia de seguridad y restauración, bloqueos, sesiones, alertas y estado del dispositivo. Se ejecuta la consola de administración en el dispositivo. los usuarios conectarse a la consola de administración a través de Internet Explorer. Para obtener más información, vea:  
  
-   [Supervisión del dispositivo mediante el uso de la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![Alertas de consola de administración PDW](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Vistas del sistema  
PDW de SQL Server incluye vistas del sistema completa que le permiten obtener información detallada sobre el estado del dispositivo, estado y rendimiento. Para obtener una lista de vistas del sistema para tareas de supervisión, consulte:  
  
-   [Supervisión del dispositivo mediante el uso de vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
PDW de SQL Server tiene una amplia integración con Systems Center Operations Manager. Los módulos de administración de PDW de SQL Server están disponibles como descarga gratuita. Para obtener más información sobre el uso de System Center para supervisar SQL Server PDW, vea lo siguiente:  
  
-   [Supervisión del dispositivo mediante el uso de System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluciones personalizadas  
Para las situaciones cuando System Center no está disponible con su centro de datos, herramientas de supervisión, puede supervisar el dispositivo mediante el uso de una solución de supervisión de terceros. Instalación de agentes de software externos no se admite en PDW, pero la mayoría de soluciones de supervisión admite Transact\-integración de SQL, por lo que el administrador del sistema puede implementar Transact directo\-consultas SQL en el PDW dispositivo.  
  
Si la solución de supervisión no es compatible con direct Transact\-consultas SQL, o si no tiene una herramienta de supervisión, a continuación, puede usar scripts para realizar tareas de supervisión, como el envío de correo electrónico cuando se produzca una alerta.  El sitio wiki de TechNet contiene un ejemplo de solución de supervisión con secuencias de comandos.  
  
-   [PowerShell de ejemplo de supervisión para SQL Server PDW](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Relacionados con tareas de supervisión  
  
|Tarea de supervisión|Descripción|  
|-------------------|---------------|  
|Supervisar el dispositivo mediante la consola de administración.|[Supervisión del dispositivo mediante el uso de la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Supervisión del dispositivo mediante el uso de vistas del sistema.|[Supervisión del dispositivo mediante el uso de vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Supervisión del dispositivo mediante el uso de System Center|[Supervisión del dispositivo mediante el uso de System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Supervisar el estado del dispositivo.|[Monitor de estado de dispositivo &#40;Analytics Platform System&#41;](monitor-appliance-health-state.md)|  
|Supervisión de latidos.|[Enviar comentarios de telemetría a Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Realizar un seguimiento de las alertas del dispositivo.|[Realizar un seguimiento de las alertas del dispositivo &#40;Analytics Platform System&#41;](track-appliance-alerts.md)|  
|Determinar cuánta capacidad se está usando.|[Uso de la capacidad de ver &#40;Analytics Platform System&#41;](view-capacity-utilization.md)|  
|Determine con qué frecuencia se sondea el dispositivo.|[Determinar la frecuencia de sondeo &#40;Analytics Platform System&#41;](determine-polling-frequency.md)|  
|Cuando se produce un error de clúster, determinar qué clúster error del nodo.|[Determine qué nodo de clúster no se pudo &#40;Analytics Platform System&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Tareas de administración de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
