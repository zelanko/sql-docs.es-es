---
title: SQL Server Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Distributed Replay
- SQL Server Distributed Replay
ms.assetid: 58ef7016-b105-42c2-90a0-364f411849a4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 583af6e77d699c88e7712ac03053467138bd5a5f
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177355"
---
# <a name="sql-server-distributed-replay"></a>SQL Server Distributed Replay
  La característica [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay le ayuda a evaluar el impacto de las actualizaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] futuras. También puede usarla para ayudar a evaluar el impacto de las actualizaciones del sistema operativo y el hardware, y de la optimización de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .

## <a name="benefits-of-distributed-replay"></a>Ventajas de Distributed Replay
 Al igual que [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], puede usar Distributed Replay para volver a consultar un seguimiento capturado contra un entorno de pruebas actualizado. A diferencia de [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)], Distributed Replay no se limita a volver a consultar la carga de trabajo de un único equipo.

 Distributed Replay proporciona una solución más escalable que [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Con Distributed Replay, puede reproducir una carga de trabajo de varios equipos y simular mejor una carga de trabajo esencial.

 La característica [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay puede usar varios equipos para reproducir los datos de seguimiento y simular una carga de trabajo esencial. Utilice Distributed Replay para probar la compatibilidad de las aplicaciones o el rendimiento, o planear la capacidad.

## <a name="when-to-use-distributed-replay"></a>Cuándo usar Distributed Replay
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] y Distributed Replay tienen algunas funciones que se solapan.

 Puede usar [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] para volver a consultar un seguimiento capturado en un entorno de pruebas actualizado. También puede analizar los resultados de la reproducción para buscar posibles incompatibilidades en el rendimiento y la funcionalidad. Sin embargo, [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] solo puede reproducir una carga de trabajo de un equipo. Al reproducir una aplicación OLTP que requiere muchos recursos y que tiene muchas conexiones simultáneas activas o un rendimiento alto, [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] se puede convertir en un cuello de botella para los recursos.

 Distributed Replay proporciona una solución más escalable que [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Use Distributed Replay para volver a reproducir una carga de trabajo de varios equipos y simular mejor una carga de trabajo esencial.

 En la siguiente tabla se describe cuándo usar cada herramienta.

|Herramienta|Usar cuando...|
|----------|---------------|
|[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]|Desea usar el mecanismo de reproducción convencional en un solo equipo. En concreto, necesita las capacidades de depuración línea por línea, como los comandos **Paso**, **Ejecutar hasta el cursor**y **Alternar punto de interrupción** .<br /><br /> Desea volver a reproducir un seguimiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|
|Distributed Replay|Desea evaluar la compatibilidad de las aplicaciones. Por ejemplo, desea probar escenarios de actualización de sistemas operativos y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , actualizaciones de hardware o la optimización de los índices.<br /><br /> La simultaneidad en el seguimiento capturado es tan alta que un solo cliente de reproducción no basta para simularla.|

## <a name="distributed-replay-concepts"></a>Conceptos de Distributed Replay
 Los siguientes componentes conforman el entorno de Distributed Replay:

-   **Herramienta de administración de Distributed Replay**: una aplicación `DReplay.exe`de consola,, que se usa para comunicarse con el controlador de reproducción distribuida. Use la herramienta de administración para controlar la reproducción distribuida.

-   **Distributed Replay Controller**: equipo que ejecuta el servicio de Windows denominado Distributed Replay Controller de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El controlador de Distributed Replay orquestra las acciones de los clientes de Distributed Replay. Solo puede haber una instancia de controlador en cada entorno de Distributed Replay.

-   **Distributed Replay Clients**: uno o varios equipos (físicos o virtuales) que ejecutan el servicio de Windows denominado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Distributed Replay Client. Los clientes de Distributed Replay colaboran para simular cargas de trabajo en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Puede haber uno o más clientes en cada entorno de Distributed Replay.

-   **Servidor de destino:** : instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que Distributed Replay Clients pueden usar para reproducir datos de seguimiento. Se recomienda que el servidor de destino se encuentre en un entorno de prueba.

 La herramienta de administración, Distributed Replay Controller y Distributed Replay Client se pueden instalar en equipos distintos o en el mismo equipo. Solo puede haber una instancia del servicio de Distributed Replay Controller o Client ejecutándose en el mismo equipo.

 La ilustración siguiente muestra la arquitectura física de Distributed Replay de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :

 ![Distributed Replay Architecture](../../database-engine/media/distributedreplayarch.gif "Distributed Replay Architecture")

## <a name="distributed-replay-tasks"></a>Tareas de Distributed Replay

|Descripción de la tarea|Tema|
|----------------------|-----------|
|Describe cómo configurar Distributed Replay.|[Configurar Distributed Replay](configure-distributed-replay.md)|
|Describe cómo preparar la información de seguimiento de entrada.|[Preparar los datos de seguimiento de entrada](prepare-the-input-trace-data.md)|
|Describe cómo reproducir los datos de seguimiento.|[Reproducir datos de seguimiento](replay-trace-data.md)|
|Describe cómo revisar los resultados de los datos de seguimiento de Distributed Replay.|[Revisar los resultados de la reproducción](review-the-replay-results.md)|
|Describe cómo usar la herramienta de administración para iniciar, supervisar y cancelar operaciones en el controlador.|[Opciones de línea de comandos de la herramienta de administración &#40;utilidad Distributed Replay&#41;](administration-tool-command-line-options-distributed-replay-utility.md)|

## <a name="see-also"></a>Consulte también
 [SQL Server Foro de Distributed Replay](https://social.technet.microsoft.com/Forums/sl/sqldru/) [con Distributed Replay para la prueba de carga de SQL Server-parte 2](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx) [con Distributed Replay para la prueba de carga de la SQL Server, parte 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)


