---
title: "Usar la sesión system_health | Microsoft Docs"
ms.custom: 
ms.date: 06/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c64a0a128576a4bbf38f10b70514dbc4def84d11
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="use-the-systemhealth-session"></a>Usar la sesión system_health
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  La sesión system_health es una sesión de eventos extendidos que se incluye de forma predeterminada con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta sesión se inicia automáticamente cuando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se inicia, y se ejecuta sin ningún efecto de rendimiento notable. La sesión recopila datos del sistema que se pueden utilizar para ayudar a solucionar problemas de rendimiento en el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por consiguiente, se recomienda no detener ni eliminar la sesión.  
  
 La sesión recopila información como la que se indica a continuación:  
  
-   sql_text y session_id para las sesiones que encuentran un error cuya gravedad es >= 20.  
  
-   sql_text y session_id para las sesiones que encuentran un error relacionado con la memoria. Entre los errores se incluyen 17803, 701, 802, 8645, 8651, 8657 y 8902.  
  
-   Un registro de los problemas de un programador que no rinde. (Estos aparecen en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como error 17883).  
  
-   Los interbloqueos detectados.  
  
-   callstack, sql_text y session_id para las sesiones que han esperado en bloqueos temporales (u otros recursos interesantes) durante > 15 segundos.  
  
-   callstack, sql_text y session_id para las sesiones que han esperado en bloqueos durante > 30 segundos.  
  
-   callstack, sql_text y session_id para las sesiones que han esperado mucho tiempo a causa de esperas preferentes. La duración varía en función del tipo de espera. Una espera preferente es aquella en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está esperando llamadas a API externas.  
  
-   La pila de llamadas y el session_id para los errores de las asignaciones virtuales y de CLR.  
  
-   Los eventos ring_buffer para el agente de memoria, el supervisor del programador, el OOM del nodo de memoria, la seguridad y la conectividad.  
  
-   Los resultados de los componentes del sistema de sp_server_diagnostics.  
  
-   Estado de la instancia recopilado por scheduler_monitor_system_health_ring_buffer_recorded.  
  
-   Errores en la asignación de CLR.  
  
-   Errores de conectividad utilizando connectivity_ring_buffer_recorded.  
  
-   Errores de seguridad utilizando security_error_ring_buffer_recorded.  
  
## <a name="viewing-the-session-data"></a>Ver los datos de la sesión  
 La sesión utiliza el destino del búfer en anillo para almacenar los datos. Para ver los datos de la sesión, utilice la siguiente consulta:  
  
```  
SELECT CAST(xet.target_data as xml) FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe  
ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
Para ver los datos de sesión del archivo de eventos, use la interfaz de usuario Eventos extendidos disponible en Management Studio. Para obtener más información, vea [Advanced Viewing of Target Data from Extended Events in SQL Server (Visualización avanzada de datos de destino de eventos extendidos en SQL Server)](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).
  
## <a name="restoring-the-systemhealth-session"></a>Restaurar la sesión system_health  
 Si elimina la sesión system_health, puede restaurarla si ejecuta el archivo **u_tables.sql** en el Editor de consultas. Este archivo se encuentra en la siguiente carpeta, donde C: representa la unidad en la que se instalaron los archivos de programa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
 C:\Archivos de programa\Microsoft SQL Server\MSSQL13.\<*id de instancia*>\MSSQL\Install  
  
 Tenga en cuenta que después de restaurar la sesión, debe iniciarla utilizando la instrucción ALTER EVENT SESSION o utilizando el nodo **Eventos extendidos** en el Explorador de objetos. De lo contrario, la sesión se iniciará automáticamente la próxima vez que se reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de eventos extendidos](../../relational-databases/extended-events/extended-events-tools.md)  
  
  

