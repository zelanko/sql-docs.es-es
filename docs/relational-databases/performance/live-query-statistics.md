---
title: Estadísticas de consulta activa | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1ea9f40ecda2d22e9117ae9156282e42b5101cd9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="live-query-statistics"></a>Estadísticas de consulta activa
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ofrece la posibilidad de ver el plan de ejecución de una consulta activa. Este plan de consulta activa ofrece información en tiempo real sobre el proceso de ejecución de consulta a medida que los controles fluyen de un [operador de plan de consulta](../../relational-databases/showplan-logical-and-physical-operators-reference.md) a otro. El plan de consulta activa muestra el progreso general de las consultas, así como estadísticas de tiempo de ejecución de nivel de operador como el número de filas, las filas generadas, el tiempo transcurrido, el progreso del operador, etc. Estos datos están disponibles en tiempo real sin necesidad de esperar a que la consulta se complete, de modo que estas estadísticas de ejecución son extremadamente útiles para depurar problemas de rendimiento de consultas. Esta característica está disponible a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], pero puede funcionar con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
> [!WARNING]  
> Esta característica sirve principalmente para solucionar problemas. Al usarla, el rendimiento general de las consultas podría bajar de forma moderada. Esta característica se puede usar con el [depurador de Transact-SQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md).  
  
#### <a name="to-view-live-query-statistics"></a>Para ver estadísticas de consultas activas  
  
1.  Para ver el plan de ejecución de consulta activa, haga clic en el icono **Estadísticas de consulta activa** del menú de herramientas.  
  
     ![Botón Estadísticas de consulta activa en la barra de herramientas](../../relational-databases/performance/media/livequerystatstoolbar.png "Botón Estadísticas de consulta activa en la barra de herramientas")  
  
     También puede tener acceso al plan de ejecución de consulta activa si hace clic con el botón derecho en una consulta seleccionada en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y, después, hace clic en **Incluir estadísticas de consultas dinámicas**.  
  
     ![Botón Estadísticas de consulta activa en el menú emergente](../../relational-databases/performance/media/livequerystatsmenu.png "Botón Estadísticas de consulta activa en el menú emergente")  
  
2.  Ejecute la consulta. El plan de consulta activa muestra el progreso general de la consulta y las estadísticas de ejecución en tiempo de ejecución (por ejemplo, el tiempo transcurrido, el progreso, etc.) de los operadores del plan de consulta. Las estadísticas de ejecución y la información de progreso de consulta se actualizan periódicamente mientras la ejecución de la consulta está en curso. Use esta información para entender el proceso de ejecución de consulta general, así como para depurar consultas de larga ejecución, consultas que se ejecutan indefinidamente, consultas que provocan un desbordamiento de tempdb y problemas de tiempo de espera.  
  
     ![Botón Estadísticas de consulta activa en el plan de presentación](../../relational-databases/performance/media/livequerystatsplan.png "Botón Estadísticas de consulta activa en el plan de presentación")  
  
 Puede tener acceso al plan de ejecución de consulta activa también desde el **Monitor de actividad** . Para ello, haga clic con el botón derecho en las consultas en la tabla **Consultas costosas activas** .  
  
 ![Botón Estadísticas de consulta activa en el Monitor de actividad](../../relational-databases/performance/media/livequerystatsactmon.png "Botón Estadísticas de consulta activa en el Monitor de actividad")  
  
## <a name="remarks"></a>Notas  
 La infraestructura de perfil de estadísticas debe estar habilitada para que las estadísticas de consulta activa puedan capturar información sobre el progreso de las consultas. Si selecciona **Incluir estadísticas de consulta activa** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , se habilita la infraestructura de estadísticas de la sesión de consulta actual. 
 
Hasta [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], existen otras dos formas de habilitar la infraestructura de estadísticas que permiten ver las estadísticas de consultas dinámicas de otras sesiones (como las del Monitor de actividad):  
  
-   Ejecute `SET STATISTICS XML ON;` o `SET STATISTICS PROFILE ON;` en la sesión de destino.  
  
 o Administrador de configuración de  
  
-   Habilite el evento extendido **query_post_execution_showplan** . Se trata de una configuración de todo el servidor que habilita las estadísticas de consulta activa en todas las sesiones. Para habilitar eventos extendidos, consulte [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).  

A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye una versión ligera de la infraestructura de perfil de estadísticas. Existen otras dos formas de habilitar la infraestructura de estadísticas ligeras que permite ver las estadísticas de consulta activa de otras sesiones (como las del Monitor de actividad):

-   Use la marca de seguimiento global 7412.  
  
 o Administrador de configuración de  
  
-   Habilitar el evento extendido **query_thread_profile** . que es una configuración de todo el servidor que habilita las estadísticas de consulta activa en todas las sesiones. Para habilitar eventos extendidos, consulte [Monitor System Activity Using Extended Events](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md).
  
 > [!NOTE]
 > No se admiten procedimientos almacenados compilados de forma nativa.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso de nivel de base de datos **SHOWPLAN** para rellenar la página de resultados de **Estadísticas de consulta activa** , el permiso de nivel de servidor **VIEW SERVER STATE** para ver las estadísticas de consulta activa y, asimismo, los permisos necesarios habituales para ejecutar consultas.  
  
## <a name="see-also"></a>Ver también  
 [Supervisar y optimizar el rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [Abrir el Monitor de actividad &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md)     
 [Monitoring Performance By Using the Query Store](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
