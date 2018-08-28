---
title: Supervisión y optimización del rendimiento | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
caps.latest.revision: 35
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2eae51e85474763dc20282c800e855172beae5ea
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43073998"
---
# <a name="monitor-and-tune-for-performance"></a>Supervisión y optimización del rendimiento
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El objetivo de supervisar bases de datos es evaluar el rendimiento de un servidor. Una supervisión eficaz implica tomar instantáneas periódicas del rendimiento actual para aislar procesos que causan problemas y recopilar datos de forma continua a lo largo del tiempo para realizar el seguimiento de las tendencias de rendimiento.  
  
 La evaluación continua del rendimiento de la base de datos ayuda a minimizar los tiempos de respuesta y a maximizar el rendimiento, obteniendo como resultado un rendimiento óptimo. El tráfico de red, la E/S de disco y el uso de la CPU eficientes son factores clave para obtener un buen rendimiento. Es necesario analizar a fondo los requisitos de las aplicaciones, comprender la estructura lógica y física de los datos, evaluar el uso de la base de datos y negociar contrapartidas, como el procesamiento de transacciones en línea (OLTP) frente a los sistemas de ayuda para la toma de decisiones.  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>Supervisión y optimización de las bases de datos para el rendimiento  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el sistema operativo Microsoft Windows proporcionan herramientas para ver las condiciones actuales de la base de datos y realizar un seguimiento del rendimiento a medida que estas cambian. Existen diversas herramientas y técnicas que puede usar para supervisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La supervisión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le ayuda a:  
  
-   Determinar si el rendimiento se puede mejorar. Por ejemplo, al supervisar los tiempos de respuesta a las consultas usadas con frecuencia, puede determinar si es necesario cambiar la consulta o los índices de las tablas.  
  
-   Evaluar la actividad de los usuarios. Por ejemplo, al supervisar usuarios que intentan conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede determinar si la seguridad está configurada correctamente y probar las aplicaciones o sistemas de desarrollo. Por ejemplo, al supervisar las consultas SQL mientras se ejecutan, puede determinar si están escritas correctamente y si producen los resultados esperados.  
  
-   Solucionar problemas o depurar componentes de aplicaciones, como procedimientos almacenados.  
  
## <a name="monitoring-in-a-dynamic-environment"></a>Supervisión en un entorno dinámico  
Las condiciones cambiantes se traducen en cambios en el rendimiento. En sus evaluaciones, los cambios de rendimiento se aprecian a medida que el número de usuarios aumenta, los métodos de acceso y conexión de los usuarios cambian, el contenido de la base de datos crece, las aplicaciones cliente cambian, los datos de las aplicaciones cambian, las consultas son más complejas y el tráfico de red crece. Usar herramientas para supervisar el rendimiento le ayuda a asociar cambios del rendimiento con las condiciones cambiantes y las consultas complejas. **Ejemplos**:  
  
-   Mediante la supervisión de los tiempos de respuesta para las consultas utilizadas con frecuencia, puede determinar si es necesario modificar la consulta o los índices de las tablas donde es necesario ejecutar las consultas.  
  
-   Mediante la supervisión de las consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] cuando se ejecutan, puede determinar si están escritas correctamente y si producen los resultados esperados.  
  
-   Mediante la supervisión de los usuarios que intentan conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede determinar si la seguridad está configurada de forma correcta y probar las aplicaciones o sistemas de desarrollo.  
  
 El tiempo de respuesta se mide como el tiempo necesario para devolver la primera fila del conjunto de resultados al usuario, en forma de confirmación visual de que se está procesando una consulta. El rendimiento es el número total de consultas controladas por el servidor durante un periodo determinado.  
  
 A medida que aumenta el número de usuarios, aumenta la competencia para obtener recursos de un servidor, y esto hace que el tiempo de respuesta aumente y el rendimiento global disminuya.  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>Tareas de supervisión y optimización del rendimiento  
  
|Tema| Tarea|  
|-----------|----------------------|  
|[Supervisar los componentes de SQL Server](../../relational-databases/performance/monitor-sql-server-components.md)|Proporciona los pasos necesarios para supervisar cualquier componente de SQL Server.|  
|[Herramientas de supervisión y optimización del rendimiento](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|Enumera las herramientas de supervisión y optimización disponibles de SQL Server.|  
|[Establecer una línea base del rendimiento](../../relational-databases/performance/establish-a-performance-baseline.md)|Proporciona información sobre cómo establecer una línea base de rendimiento.|  
|[Aislar problemas de rendimiento](../../relational-databases/performance/isolate-performance-problems.md)|Describe cómo aislar problemas de rendimiento de base de datos.|  
|[Identificar los cuellos de botella](../../relational-databases/performance/identify-bottlenecks.md)|Describe cómo supervisar y seguir el rendimiento del servidor para identificar cuellos de botella.|  
|[Supervisión de la actividad y el rendimiento del servidor](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|Describe cómo usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las herramientas de supervisión de rendimiento y actividad de Windows.|  
|[Mostrar y guardar planes de ejecución](../../relational-databases/performance/display-and-save-execution-plans.md)|Describe cómo mostrar y guardar planes de ejecución en un archivo de formato XML.|  
|[Estadísticas de consultas activas](../../relational-databases/performance/live-query-statistics.md)|Muestra estadísticas en tiempo real sobre los pasos de ejecución de consultas.|  
|[Supervisar el rendimiento mediante el almacén de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|El almacén de consultas captura automáticamente un historial de consultas, planes y estadísticas en tiempo de ejecución, y las conserva para su revisión.|  
|[Uso del almacén de consultas con OLTP en memoria](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)|Consideraciones sobre tablas con optimización para memoria.|  
|[Procedimiento recomendado con el Almacén de consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)|Se proporcionan consejos sobre cómo usar el Almacén de consultas.|  
  
## <a name="see-also"></a>Vea también  
 [Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)   
 [Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
