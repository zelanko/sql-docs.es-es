---
title: Supervisión y optimización del rendimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 683e8044b235828741fe429f133af82d1977031a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63150715"
---
# <a name="monitor-and-tune-for-performance"></a>Supervisión y optimización del rendimiento
  El objetivo de supervisar bases de datos es evaluar el rendimiento de un servidor. Una supervisión eficaz implica tomar instantáneas periódicas del rendimiento actual para aislar procesos que causan problemas y recopilar datos de forma continua a lo largo del tiempo para realizar el seguimiento de las tendencias de rendimiento.  
  
 La evaluación continua del rendimiento de la base de datos ayuda a minimizar los tiempos de respuesta y a maximizar el rendimiento, obteniendo como resultado un rendimiento óptimo. El tráfico de red, la E/S de disco y el uso de la CPU eficientes son factores clave para obtener un buen rendimiento. Es necesario analizar a fondo los requisitos de las aplicaciones, comprender la estructura lógica y física de los datos, evaluar el uso de la base de datos y negociar contrapartidas, como el procesamiento de transacciones en línea (OLTP) frente a los sistemas de ayuda para la toma de decisiones.  
  
## <a name="benefits-of-monitoring-and-tuning-databases-for-performance"></a>Ventajas de las bases de datos de supervisión y optimización del rendimiento  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el sistema operativo Microsoft Windows proporcionan herramientas que le permiten ver las condiciones actuales de la base de datos y realizar un seguimiento del rendimiento a medida que estas cambian. Existen diversas herramientas y técnicas que se pueden utilizar para supervisar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Conocer el modo de supervisar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ayudarle a:  
  
-   Determinar si el rendimiento se puede mejorar. Por ejemplo, al supervisar los tiempos de respuesta a las consultas usadas con frecuencia, puede determinar si es necesario cambiar la consulta o los índices de las tablas.  
  
-   Evaluar la actividad de los usuarios. Por ejemplo, al supervisar usuarios que intentan conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede determinar si la seguridad está configurada correctamente y probar las aplicaciones o sistemas de desarrollo. Por ejemplo, al supervisar las consultas SQL mientras se ejecutan, puede determinar si están escritas correctamente y si producen los resultados esperados.  
  
-   Solucionar problemas o depurar componentes de aplicaciones, como procedimientos almacenados.  
  
### <a name="monitoring-in-a-dynamic-environment"></a>Supervisión en un entorno dinámico  
 La supervisión es importante, puesto que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece un servicio en un entorno dinámico. Las condiciones cambiantes se traducen en cambios en el rendimiento. En sus evaluaciones, los cambios de rendimiento se aprecian a medida que el número de usuarios aumenta, los métodos de acceso y conexión de los usuarios cambian, el contenido de la base de datos crece, las aplicaciones cliente cambian, los datos de las aplicaciones cambian, las consultas son más complejas y el tráfico de red crece. Con la ayuda de las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para supervisar el rendimiento, puede asociar algunos cambios del rendimiento con las condiciones cambiantes y las consultas complejas. A continuación se muestran algunos escenarios a modo de ejemplo:  
  
-   Mediante la supervisión de los tiempos de respuesta para las consultas utilizadas con frecuencia, puede determinar si es necesario modificar la consulta o los índices de las tablas donde es necesario ejecutar las consultas.  
  
-   Mediante la supervisión de las consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] cuando se ejecutan, puede determinar si están escritas correctamente y si producen los resultados esperados.  
  
-   Mediante la supervisión de los usuarios que intentan conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede determinar si la seguridad está configurada de forma correcta y probar las aplicaciones o sistemas de desarrollo.  
  
 El tiempo de respuesta se mide como el tiempo necesario para devolver la primera fila del conjunto de resultados al usuario, en forma de confirmación visual de que se está procesando una consulta. El rendimiento es el número total de consultas controladas por el servidor durante un periodo determinado.  
  
 A medida que aumenta el número de usuarios, aumenta la competencia para obtener recursos de un servidor, y esto hace que el tiempo de respuesta aumente y el rendimiento global disminuya.  
  
## <a name="monitoring-and-tuning-performance-tasks"></a>Tareas de supervisión y optimización del rendimiento  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|[Supervisar los componentes de SQL Server](monitor-sql-server-components.md)|Proporciona los pasos necesarios para supervisar eficazmente cualquier componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Herramientas de optimización y supervisión del rendimiento](performance-monitoring-and-tuning-tools.md)|Enumera las herramientas de supervisión y optimización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Establecer una línea base del rendimiento](establish-a-performance-baseline.md)|Proporciona información acerca de cómo establecer una línea base de rendimiento.|  
|[Aislar problemas de rendimiento](isolate-performance-problems.md)|Describe cómo aislar problemas de rendimiento de base de datos.|  
|[Identificar los cuellos de botella](identify-bottlenecks.md)|Describe cómo supervisar y seguir el rendimiento del servidor para identificar cuellos de botella.|  
|[Supervisión de la actividad y rendimiento del servidor](server-performance-and-activity-monitoring.md)|Describe cómo usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las herramientas de supervisión de rendimiento y actividad de Windows.|  
|[Mostrar y guardar planes de ejecución](display-and-save-execution-plans.md)|Describe cómo mostrar y guardar planes de ejecución en un archivo de formato XML.|  
|[Supervisar el rendimiento mediante el Almacén de consultas](monitoring-performance-by-using-the-query-store.md)|El almacén de consultas captura automáticamente un historial de consultas, planes y estadísticas en tiempo de ejecución las conserva para su revisión.|  
  
## <a name="see-also"></a>Consulte también  
 [Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)   
 [Asistente para la optimización de motor de base de datos](database-engine-tuning-advisor.md)   
 [Supervisar el uso de recursos &#40;el monitor de sistema&#41;](../performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
