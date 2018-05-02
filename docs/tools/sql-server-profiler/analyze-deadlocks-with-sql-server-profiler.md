---
title: Analizar interbloqueos con SQL Server Profiler | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: sql-server-profiler
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- process nodes [SQL Server Profiler]
- Profiler [SQL Server Profiler], deadlocks
- deadlocks [SQL Server], identifying cause
- resource nodes [SQL Server Profiler]
- graphs [SQL Server Profiler]
- SQL Server Profiler, deadlocks
- events [SQL Server], deadlocks
- edges [SQL Server Profiler]
ms.assetid: 72d6718f-501b-4ea6-b344-c0e653f19561
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2fc7e2adc786982611e58ca4083c575902e5aca3
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="analyze-deadlocks-with-sql-server-profiler"></a>Analizar interbloqueos con SQL Server Profiler
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para identificar la causa de un interbloqueo. Un interbloqueo se produce cuando hay una dependencia cíclica entre dos o más subprocesos o procesos para algún conjunto de recursos en SQL Server. El [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]le permite crear un seguimiento que registra, reproduce y muestra eventos de interbloqueo para su análisis.  
  
 Para realizar un seguimiento de los eventos de interbloqueo, agregue la clase de evento **Deadlock graph** a un seguimiento. Esta clase de evento rellena la columna de datos **TextData** del seguimiento con datos XML acerca de los procesos y objetos implicados en el interbloqueo. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pueden extraer el documento XML a un archivo XML de interbloqueo (.xdl) que puede ver después en SQL Server Management Studio. Puede configurar el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para extraer eventos **Deadlock graph** en un solo archivo que contenga todos los eventos **Deadlock graph** o en archivos independientes. Esta extracción se puede hacer de las siguientes formas:  
  
-   Al configurar el seguimiento, mediante la pestaña **Configuración de extracción de eventos** . Tenga en cuenta que esta pestaña no aparece hasta que haya seleccionado el evento **Deadlock graph** en la pestaña **Selección de eventos** .  
  
-   Mediante la opción **Extraer eventos de SQL Server** del menú **Archivo** .  
  
-   También puede extraer y guardar eventos individuales al hacer clic con el botón derecho en un evento concreto y elegir **Extraer datos de evento**.  
  
## <a name="deadlock-graphs"></a>Gráficos de interbloqueo  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usan un gráfico de espera de interbloqueo para describir un interbloqueo. El gráfico de espera de interbloqueo contiene nodos de proceso, nodos de recurso y bordes que representan las relaciones entre los procesos y los recursos. Los componentes de los gráficos de espera se definen en la siguiente tabla:  
  
 Nodo de proceso  
 Un subproceso que realiza una tarea; por ejemplo, INSERT, UPDATE o DELETE.  
  
 Nodo de recurso  
 Un objeto de la base de datos; por ejemplo, una tabla, un índice o una fila.  
  
 Borde  
 Una relación entre un proceso y un recurso. Un borde **request** se produce cuando un proceso espera un recurso. Un borde **owner** se produce cuando un recurso espera un proceso. El modo de bloqueo se incluye en la descripción del borde. Por ejemplo, **Modo: X**.  
  
## <a name="deadlock-process-node"></a>Nodo de proceso de interbloqueo  
 En un gráfico de espera, el nodo de proceso contiene información acerca del proceso. En la tabla siguiente se explican los componentes de un proceso.  
  
|Componente|Definición|  
|---------------|----------------|  
|Id. de proceso de servidor|Identificador de proceso de servidor (SPID), un identificador asignado a un servidor para el proceso que posee el bloqueo.|  
|Id. de lote de servidores|Identificador de lote de servidores (SBID).|  
|Id. de contexto de ejecución|Identificador de contexto de ejecución (ECID). Id. de contexto de ejecución de un subproceso dado asociado con un SPID específico.<br /><br /> ECID = {0,1,2,3, *...n*}, donde 0 siempre representa el subproceso principal o primario, y {1,2,3, *...n*} representan los subprocesos secundarios.|  
|Prioridad de interbloqueo|Prioridad de interbloqueo del proceso. Para obtener más información sobre los valores posibles, vea [SET DEADLOCK_PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/set-deadlock-priority-transact-sql.md).|  
|Registro utilizado|Cantidad de espacio del registro utilizado por el proceso.|  
|Id. de propietario|Id. de transacción de los procesos que están usando transacciones y que actualmente están esperando en un bloqueo.|  
|Descriptor de transacción|Puntero al descriptor de transacción que describe el estado de la transacción.|  
|Búfer de entrada|Búfer de entrada del proceso actual; define el tipo de evento y la instrucción que se está ejecutando. Los valores posibles incluyen:<br /><br /> **Lenguaje**<br /><br /> **RPC**<br /><br /> **Ninguno**|  
|.|Tipo de instrucción. Los valores posibles son:<br /><br /> **NOP**<br /><br /> **SELECT**<br /><br /> **UPDATE**<br /><br /> **INSERT**<br /><br /> **DELETE**<br /><br /> **Desconocido**|  
  
## <a name="deadlock-resource-node"></a>Nodo de recurso de interbloqueo  
 En un interbloqueo, dos procesos están esperando un recurso retenido por el otro recurso. En un gráfico de interbloqueo, los recursos se muestran como nodos de recursos.  
  
  
