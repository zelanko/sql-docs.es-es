---
title: Supervisión de los componentes de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: e8f1b16b-ea40-4e12-886c-967ebda4e6e4
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: bacf9a8a08008b23309d2d8c08b9310c491abf2a
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2019
ms.locfileid: "55087684"
---
# <a name="monitor-sql-server-components"></a>Supervisar los componentes de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La supervisión es importante, puesto que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece un servicio en un entorno dinámico. Los datos de la aplicación cambian. El tipo de acceso que requieren los usuarios cambia. La forma de conexión de los usuarios cambia. También pueden cambiar los tipos de aplicaciones que tienen acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra automáticamente los recursos del sistema, como la memoria y el espacio en disco, para minimizar la necesidad de optimizar manualmente el sistema. La supervisión permite a los administradores identificar las tendencias de funcionamiento para determinar si es necesario realizar cambios.  
  
Para supervisar cualquier componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eficazmente:  
  
1.  Defina los objetivos de supervisión.  
2.  Seleccione la herramienta apropiada.    
3.  Identifique los componentes que desea supervisar.  
4.  Seleccione métricas para dichos componentes.  
5.  Supervise el servidor.  
6.  Analice los datos.  
  
Estos pasos se tratan más extensamente a continuación.  
  
## <a name="determine-your-monitoring-goals"></a>Defina los objetivos de supervisión  
Para supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de forma eficaz, debe identificar claramente los motivos de la supervisión. Entre los motivos se pueden incluir los siguientes:  
  
-   Establecer una línea de base para el rendimiento.  
-   Identificar los cambios del rendimiento a lo largo del tiempo.  
-   Diagnosticar problemas de rendimiento concretos.  
-   Identificar componentes o procesos para optimizar.  
-   Comparar las consecuencias de distintas aplicaciones cliente sobre el rendimiento.  
-   Llevar a cabo auditorías de la actividad de los usuarios.  
-   Probar un servidor con cargas distintas.  
-   Probar la arquitectura de las bases de datos.  
-   Probar distintas programaciones de mantenimiento.  
-   Probar los planes de copias de seguridad y restauración.  
-   Determinar cuándo se ha de modificar la configuración de hardware.  
  
## <a name="select-the-appropriate-tool"></a>Seleccione la herramienta apropiada  
Después de decidir los motivos de la supervisión, debe seleccionar las herramientas adecuadas para ese tipo de supervisión. El sistema operativo Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrecen un conjunto completo de herramientas para supervisar servidores en entornos con muchas transacciones. Estas herramientas revelan claramente las condiciones de una instancia del motor de base de datos de SQL Server o de una instancia de SQL Server Analysis Services.  
  
Windows ofrece las herramientas siguientes para supervisar aplicaciones que se ejecutan en un servidor:  
  
-   [Monitor del sistema](../../relational-databases/performance/start-system-monitor-windows.md), que permite recopilar y ver datos en tiempo real sobre actividades como el uso de memoria, disco y procesador.  
-   Registros y alertas de rendimiento  
-   Administrador de tareas  
  
Para obtener más información acerca de las herramientas de Windows o Windows Server, vea la documentación de Windows.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece las herramientas siguientes para supervisar componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)
-   [Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)  
-   [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
-   [Utilidad de reproducción distribuida](../../tools/distributed-replay/sql-server-distributed-replay.md)  
-   [Monitor de actividad](../../relational-databases/performance-monitor/activity-monitor.md)  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Plan de presentación gráfico de  
-   [Procedimientos almacenados del sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
-   [Comandos de consola de base de datos (DBCC)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
-   [Funciones y vistas de administración dinámica](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
-   [Funciones](../../t-sql/functions/functions.md)   
-   [Marcas de seguimiento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)   

> [!IMPORTANT]
> Seguimiento de SQL y [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] están en desuso. El espacio de nombres *Microsoft.SqlServer.Management.Trace* que contiene los objetos Trace y Replay de Microsoft SQL Server también están en desuso. 
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 
> Use eventos extendidos en su lugar. Para más información sobre los [eventos extendidos](../../relational-databases/extended-events/extended-events.md), vea [Inicio rápido: Eventos extendidos en SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) y [Generador de perfiles XEvent de SSMS](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md).

> [!NOTE]
> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para las cargas de trabajo de Analysis Services NO está en desuso y seguirá siendo compatible.

Para obtener más información sobre las herramientas de supervisión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md).  
  
## <a name="identify-the-components-to-monitor"></a>Identifique los componentes que desea supervisar  
El tercer paso para supervisar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es identificar los componentes que desea supervisar. Por ejemplo, si utiliza [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para realizar el seguimiento de un servidor, puede definir el seguimiento para que recopile datos de eventos concretos. También puede excluir eventos que no se apliquen a su situación.  
  
## <a name="select-metrics-for-monitored-components"></a>Seleccione métricas para los componentes supervisados  
Después de identificar qué componentes va a supervisar, determine las métricas de estos componentes. Por ejemplo, después de elegir los eventos que se van a incluir en un seguimiento, puede decidir incluir solo datos concretos acerca de los eventos. Al limitar el seguimiento a los datos relevantes para el mismo, se minimizan los recursos del sistema necesarios para realizar el seguimiento.  
  
## <a name="monitor-the-server"></a>Supervise el servidor  
Para supervisar el servidor, ejecute la herramienta de supervisión que ha configurado para recopilar datos. Por ejemplo, después de definir un seguimiento, puede ejecutarlo para recopilar datos acerca de eventos que ocurran en el servidor.  

## <a name="analyze-the-data"></a>Analice los datos  
Una vez haya finalizado el seguimiento, analice los datos para ver si ha alcanzado su objetivo de supervisión. Si no lo ha alcanzado, modifique los componentes o las métricas utilizadas para supervisar el servidor.  
  
A continuación se describe el proceso de captura y uso de datos de eventos.  
  
1.  Aplique filtros para limitar los datos de eventos que va a recopilar.  
  
    Si limita los datos de eventos, permitirá al sistema centrarse en los eventos pertinentes en el escenario de supervisión. Por ejemplo, si desea supervisar consultas lentas, puede utilizar un filtro para supervisar únicamente las consultas emitidas por la aplicación que tarden más de 30 segundos en ejecutarse en una base de datos determinada. 
    
    Para más información sobre cómo filtrar los eventos extendidos, vea [Inicio rápido: eventos extendidos en SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md#demo-of-ssms-integration). 
    
    Para obtener más información sobre el filtrado de Seguimiento de SQL, vea [Establecer un filtro de seguimiento &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md) y [Filtrar eventos en un seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md).  
  
2.  Supervise (capture) eventos.  
  
    Una vez habilitada, la supervisión activa captura datos de la aplicación, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o el sistema operativo especificados. Por ejemplo, cuando se supervisa la actividad de disco mediante el Monitor de sistema, la supervisión captura datos de eventos, como las lecturas y escrituras de disco, y los muestra en pantalla. Para obtener más información, vea [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
3.  Guarde los datos de eventos capturados.  
  
    Al guardar datos de eventos capturados, puede analizarlos posteriormente. Los datos de eventos capturados se guardan en un archivo que se puede volver a cargar en la herramienta con que se creó para el análisis. El almacenamiento de los datos de eventos capturados es importante cuando se crea una línea base de rendimiento. Los datos de la línea base de rendimiento se guardan y se utilizan, al comparar datos de eventos capturados recientemente, a fin de determinar si el rendimiento es óptimo.
    
    Los Eventos extendidos permiten guardar datos de eventos en un archivo de eventos, contador de eventos, histograma y búfer en anillo. Para obtener más información, vea [Destinos para eventos extendidos en SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md).
    
    Los datos de eventos de seguimiento de SQL incluso se pueden reproducir mediante la Utilidad de reproducción distribuida o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] permite guardar los datos de eventos en un archivo o una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Plantillas y permisos de SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md).  
  
4.  Cree plantillas de seguimiento que contengan la configuración especificada para capturar los eventos.  
  
    Las plantillas de seguimiento incluyen especificaciones acerca de los eventos, los datos de eventos y los filtros que se utilizarán para capturar datos. Puede utilizar estas plantillas para supervisar más tarde un conjunto específico de eventos, sin necesidad de volver a definir los eventos, los datos de los eventos ni los filtros. Por ejemplo, si desea supervisar a menudo el número de interbloqueos, y los usuarios implicados en estos interbloqueos, puede crear una plantilla que defina estos eventos, los datos y los filtros de eventos, guardar la plantilla y volver a aplicar el filtro la próxima vez que desee supervisar los interbloqueos.
    
    Una definición de sesión de Eventos extendidos es una plantilla que se puede incluir en un script y volver a usarse. Para crear y administrar sesiones, vea [Administración de sesiones de eventos en el Explorador de objetos](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md). El Generador de eventos XEvent de [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] ya proporciona plantillas que están listas para usarse. Para obtener más información, vea [Uso de XEvent Profiler de SSMS](../../relational-databases/extended-events/use-the-ssms-xe-profiler.md).
       
    [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] usa las plantillas de seguimiento con este fin. Para obtener más información, vea [Configurar los valores predeterminados de definición de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md) y [Crear una plantilla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/create-a-trace-template-sql-server-profiler.md).  
    
    > [!TIP]
    > Una definición de seguimiento de SQL se puede convertir en una sesión de eventos extendidos. Para obtener más información, vea [Conversión de un script de seguimiento de SQL existente en una sesión de eventos extendidos](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md).
  
5.  Analice los datos de eventos capturados.  
  
     Para analizar los datos de eventos capturados, es necesario cargarlos en la aplicación con que se capturaron. 
     
     Por ejemplo, un seguimiento de evento extendido capturado se puede volver a cargar en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para verlo y analizarlo. Para obtener más información, vea [Advanced Viewing of Target Data from Extended Events in SQL Server (Visualización avanzada de datos de destino de eventos extendidos en SQL Server)](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).

     Los datos de Seguimiento SQL se pueden volver a cargar en [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para verlos y analizarlos. Para obtener más información, vea [Ver y analizar seguimientos con SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md).  
  
     El análisis de los datos de eventos conlleva determinar qué sucede y por qué. Esta información permite realizar cambios para mejorar el rendimiento, como agregar memoria, cambiar índices, corregir problemas de códigos con procedimientos almacenados o instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)], etc., en función del tipo de análisis realizado. Por ejemplo, se puede usar el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para analizar un seguimiento capturado de Eventos extendidos o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], y hacer recomendaciones de indexación en función de los resultados.  
  
6.  Reproduzca los datos de los eventos capturados (opcional).  
  
     La reproducción de eventos permite establecer una copia de prueba del entorno de base de datos en el que se capturaron los datos y, a continuación, repetir los eventos capturados tal y como ocurrieron originalmente en el sistema real. Esta capacidad solo está disponible con la utilidad de reproducción distribuida o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Puede reproducir los eventos a la velocidad original, a la mayor velocidad posible (para intensificar el uso del sistema) o paso a paso (el tipo de reproducción más frecuente) para analizar el sistema después de que haya ocurrido cada evento. Al analizar los eventos exactos de un entorno de pruebas, puede evitar daños en el sistema de producción. Para obtener más información, vea [Reproducir seguimientos](../../tools/sql-server-profiler/replay-traces.md).  
  
  
