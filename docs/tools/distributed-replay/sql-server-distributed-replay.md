---
title: SQL Server Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Distributed Replay
- SQL Server Distributed Replay
ms.assetid: 58ef7016-b105-42c2-90a0-364f411849a4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f71b19977746ecc52817fa0128d6f0a8e681ff5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949918"
---
# <a name="sql-server-distributed-replay"></a>SQL Server Distributed Replay
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La característica Distributed Replay de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le ayuda a evaluar el impacto de las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] futuras. También puede usarla para ayudar a evaluar el impacto de las actualizaciones del sistema operativo y el hardware, y de la optimización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="benefits-of-distributed-replay"></a>Ventajas de Distributed Replay  
 Al igual que [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], puede usar Distributed Replay para volver a consultar un seguimiento capturado contra un entorno de pruebas actualizado. A diferencia de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], Distributed Replay no se limita a volver a consultar la carga de trabajo de un único equipo.  
  
 Distributed Replay proporciona una solución más escalable que [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Con Distributed Replay, puede reproducir una carga de trabajo de varios equipos y simular mejor una carga de trabajo esencial.  
  
 La característica [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay puede usar varios equipos para reproducir los datos de seguimiento y simular una carga de trabajo esencial. Utilice Distributed Replay para probar la compatibilidad de las aplicaciones o el rendimiento, o planear la capacidad.  
  
## <a name="when-to-use-distributed-replay"></a>Cuándo usar Distributed Replay  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y Distributed Replay tienen algunas funciones que se solapan.  
  
 Puede usar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para volver a consultar un seguimiento capturado en un entorno de pruebas actualizado. También puede analizar los resultados de la reproducción para buscar posibles incompatibilidades en el rendimiento y la funcionalidad. Sin embargo, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] solo puede reproducir una carga de trabajo de un equipo. Al reproducir una aplicación OLTP que requiere muchos recursos y que tiene muchas conexiones simultáneas activas o un rendimiento alto, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] se puede convertir en un cuello de botella para los recursos.  
  
 Distributed Replay proporciona una solución más escalable que [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Use Distributed Replay para volver a reproducir una carga de trabajo de varios equipos y simular mejor una carga de trabajo esencial.  
  
 En la siguiente tabla se describe cuándo usar cada herramienta.  
  
|Herramienta|Usar cuando...|  
|----------|---------------|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]|Desea usar el mecanismo de reproducción convencional en un solo equipo. En concreto, necesita las capacidades de depuración línea por línea, como los comandos **Paso**, **Ejecutar hasta el cursor**y **Alternar punto de interrupción** .<br /><br /> Desea volver a reproducir un seguimiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Distributed Replay|Desea evaluar la compatibilidad de las aplicaciones. Por ejemplo, desea probar escenarios de actualización de sistemas operativos y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , actualizaciones de hardware o la optimización de los índices.<br /><br /> La simultaneidad en el seguimiento capturado es tan alta que un solo cliente de reproducción no basta para simularla.|  
  
## <a name="distributed-replay-concepts"></a>Conceptos de Distributed Replay  
 Los siguientes componentes conforman el entorno de Distributed Replay:  
  
-   **Herramienta de administración de Distributed Replay**: una aplicación de consola, **DReplay.exe**, que se usa para comunicarse con Distributed Replay Controller. Use la herramienta de administración para controlar la reproducción distribuida.  
  
-   **Distributed Replay Controller**: equipo que ejecuta el servicio de Windows denominado Distributed Replay Controller de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El controlador de Distributed Replay orquestra las acciones de los clientes de Distributed Replay. Solo puede haber una instancia de controlador en cada entorno de Distributed Replay.  
  
-   **Distributed Replay Clients**: uno o varios equipos (físicos o virtuales) que ejecutan el servicio de Windows denominado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client. Los clientes de Distributed Replay colaboran para simular cargas de trabajo en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede haber uno o más clientes en cada entorno de Distributed Replay.  
  
-   **Servidor de destino**: instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que Distributed Replay Clients pueden usar para reproducir datos de seguimiento. Se recomienda que el servidor de destino se encuentre en un entorno de prueba.  
  
 La herramienta de administración, Distributed Replay Controller y Distributed Replay Client se pueden instalar en equipos distintos o en el mismo equipo. Solo puede haber una instancia del servicio de Distributed Replay Controller o Client ejecutándose en el mismo equipo.  
  
 La ilustración siguiente muestra la arquitectura física de Distributed Replay de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
 ![Arquitectura de Distributed Replay](../../tools/distributed-replay/media/distributedreplayarch.gif "Arquitectura de Distributed Replay")  
  
## <a name="distributed-replay-tasks"></a>Tareas de Distributed Replay  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo configurar Distributed Replay.|[Configurar Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)|  
|Describe cómo preparar la información de seguimiento de entrada.|[Preparar los datos de seguimiento de entrada](../../tools/distributed-replay/prepare-the-input-trace-data.md)|  
|Describe cómo reproducir los datos de seguimiento.|[Reproducir datos de seguimiento](../../tools/distributed-replay/replay-trace-data.md)|  
|Describe cómo revisar los resultados de los datos de seguimiento de Distributed Replay.|[Revisar los resultados de la reproducción](../../tools/distributed-replay/review-the-replay-results.md)|  
|Describe cómo usar la herramienta de administración para iniciar, supervisar y cancelar operaciones en el controlador.|[Opciones de línea de comandos de la herramienta de administración &#40;utilidad Distributed Replay&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Foro de SQL Server Distributed Replay](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Usar Distributed Replay para la prueba de carga de SQL Server, parte 2](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Usar Distributed Replay para la prueba de carga de SQL Server, parte 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
