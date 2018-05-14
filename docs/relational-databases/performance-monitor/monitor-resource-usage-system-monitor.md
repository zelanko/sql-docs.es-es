---
title: Supervisión del uso de recursos (Monitor de sistema) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server], resource usage
- System Monitor [SQL Server], about Windows System Monitor
- resource usage monitoring [SQL Server]
- System Monitor [SQL Server]
- counters [SQL Server], resource usage subjects
- performance counters [SQL Server], resource usage subjects
- Windows System Monitor [SQL Server], about Windows System Monitor
- monitoring [SQL Server], server resource usage
- monitoring resource usage [SQL Server]
- Windows System Monitor [SQL Server]
- database monitoring [SQL Server], resource usage
- database performance [SQL Server], resource usage
- tuning databases [SQL Server], resource usage
- server performance [SQL Server], resource usage
ms.assetid: f2993a28-0b81-46f2-aec0-6877fe990387
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 541d98f630c49acc778594b05fd71f4e9220fe8f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-resource-usage-system-monitor"></a>Supervisar el uso de recursos (Monitor de sistema)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si está ejecutando el sistema operativo de servidor de Microsoft Windows, utilice la herramienta gráfica Monitor de sistema para medir el rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede ver los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los contadores de rendimiento y el comportamiento de otros objetos, como procesadores, memoria, caché, subprocesos y procesos. Cada uno de estos objetos tiene asociado un conjunto de contadores que miden el uso de los dispositivos, la longitud de las colas, las demoras y otros indicadores del rendimiento y la congestión interna.  
  
> [!NOTE]  
>  El Monitor de sistema ha reemplazado al Monitor de rendimiento después de Windows NT 4.0.  
  
## <a name="benefits-of-system-monitor"></a>Ventajas del Monitor de sistema  
 El Monitor de sistema puede resultar útil para supervisar el sistema operativo Windows y los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al mismo tiempo con el fin de determinar las posibles correlaciones entre el rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el de Windows. Por ejemplo, la supervisión simultánea de los contadores de E/S de disco de Windows y los contadores del Administrador de búfer de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede mostrar el comportamiento del sistema en su totalidad.  
  
 El Monitor de sistema permite obtener estadísticas sobre la actividad y el rendimiento actuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Con el Monitor de sistema, puede:  
  
-   Ver simultáneamente datos de cualquier número de equipos.  
  
-   Ver y cambiar gráficos para reflejar la actividad actual y mostrar valores de contadores que se actualizan con la frecuencia definida por el usuario.  
  
-   Exportar datos desde gráficos, registros, registros de alertas e informes a aplicaciones de hoja de cálculo o de base de datos para manipularlos e imprimirlos.  
  
-   Agregar alertas del sistema que muestran un evento en el registro de alertas y que pueden notificarse mediante una alerta de red.  
  
-   Ejecutar un programa predefinido la primera vez, o todas las veces, que el valor de un contador sea superior o inferior a un valor definido por el usuario.  
  
-   Crear archivos de registro que contengan datos relativos a diversos objetos de equipos diferentes.  
  
-   Anexar a un archivo secciones seleccionadas de otros archivos de registro existentes para crear un archivo de almacenamiento a largo plazo.  
  
-   Ver informes de la actividad actual o crear informes a partir de archivos de registro existentes.  
  
-   Guardar la configuración de gráficos, alertas, registros o informes individuales, o bien de toda el área de trabajo, para volverla a utilizar.  
  
    > [!NOTE]  
    >  El Monitor de sistema ha reemplazado al Monitor de rendimiento después de Windows NT 4.0. Para realizar estas tareas, puede utilizar el Monitor de sistema o el Monitor de rendimiento.  
  
## <a name="system-monitor-performance"></a>Rendimiento del Monitor de sistema  
 Al supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el sistema operativo Microsoft Windows para investigar problemas relacionados con el rendimiento, hay tres áreas principales en las que debe concentrarse inicialmente:  
  
-   Actividad del disco  
  
-   Uso del procesador  
  
-   Uso de la memoria  
  
 La supervisión de un equipo en el que se ejecuta el Monitor de sistema puede afectar un poco al rendimiento del equipo. Por tanto, registre los datos del Monitor de sistema en otro disco o en otro equipo para reducir así el efecto en el equipo que está supervisando, o bien ejecute el Monitor de sistema desde un equipo remoto. Supervise solo los contadores en los que esté interesado. Si supervisa demasiados contadores, la sobrecarga de uso de los recursos se agrega al proceso de supervisión y afecta al rendimiento del equipo que se está supervisando.  
  
## <a name="system-monitor-tasks"></a>Tareas del Monitor de sistema  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cuándo debe usarse el Monitor de sistema y explica la sobrecarga de rendimiento derivada del uso del Monitor de sistema.|[Ejecutar Monitor de sistema](../../relational-databases/performance-monitor/run-system-monitor.md)|  
|Describe cómo deben supervisarse los contadores de disco para determinar la actividad del disco y la cantidad de actividad de E/S que generan los componentes de SQL Server.|[Supervisar el uso del disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)|  
|Describe cómo se supervisa una instancia de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para determinar si los índices de uso de la CPU son normales.|[Supervisar el uso de la CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)|  
|Describe cómo se supervisa una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para confirmar que el uso de la memoria se encuentra dentro de los rangos normales.|[Supervisar el uso de la memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)|  
|Describe cómo se crea una alerta que se activará cuando se alcance un valor de umbral en un contador del Monitor del sistema.|[Crear una alerta de base de datos de SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)|  
|Describe cómo se crean gráficos, alertas, registros e informes para supervisar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Crear gráficos, alertas, registros e informes](../../relational-databases/performance-monitor/create-charts-alerts-logs-and-reports.md)|  
|Muestra los objetos y contadores que el Monitor del sistema usa para supervisar la actividad de los equipos en los que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)|  
|Muestra los objetos y contadores que el Monitor del sistema usa para supervisar la actividad de OLTP en memoria.|[Contadores de rendimiento de XTP &#40;OLTP en memoria&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)|  
  
  
