---
title: Usar la sesión system_health
description: La sesión de eventos extendidos system_health se incluye con SQL Server. Esta sesión recopila datos del sistema para solucionar problemas de rendimiento del motor de base de datos.
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ffa5587415d9f4bc689a37a5ba49be87eaf14716
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "79487593"
---
# <a name="use-the-system_health-session"></a>Usar la sesión system_health

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La sesión system_health es una sesión de eventos extendidos que se incluye de forma predeterminada con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta sesión se inicia automáticamente cuando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se inicia, y se ejecuta sin ningún efecto de rendimiento notable. La sesión recopila datos del sistema que se pueden utilizar para ayudar a solucionar problemas de rendimiento en el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. 

> [!IMPORTANT]
> Se recomienda no detener, alterar ni eliminar la sesión de estado del sistema. Es posible que una actualización futura del producto sobrescriba cualquier cambio realizado en la configuración de sesión de system_health.
  
La sesión recopila información como la que se indica a continuación:  
  
-   Los valores *sql_text* y *session_id* para las sesiones que encuentran un error cuya gravedad es >= 20.  
  
-   Los valores *sql_text* y *session_id* para las sesiones que encuentran un error relacionado con la memoria. Entre los errores se incluyen 17803, 701, 802, 8645, 8651, 8657 y 8902.  
  
-   Un registro de los problemas de un programador que no rinde. Estos aparecen en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como error 17883.  
  
-   Los interbloqueos que se detectan, incluido el gráfico de interbloqueo.  
  
-   Los valores *callstack*, *sql_text* y *session_id* para las sesiones que han esperado en bloqueos temporales (u otros recursos interesantes) durante > 15 segundos.  
  
-   Los valores *callstack*, *sql_text* y *session_id* para las sesiones que han esperado en bloqueos durante > 30 segundos.  
  
-   Los valores *callstack*, *sql_text* y *session_id* para las sesiones que han esperado mucho tiempo esperas preferentes. La duración varía en función del tipo de espera. Una espera preferente es aquella en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está esperando llamadas a API externas.  
  
-   Los valores *callstack* y *session_id* para los errores de las asignaciones virtuales y de CLR.  
  
-   Los eventos del búfer en anillo para el agente de memoria, el supervisor del programador, el OOM del nodo de memoria, la seguridad y la conectividad.  
  
-   Resultados de componente del sistema de `sp_server_diagnostics`.  
  
-   Estado de la instancia recopilado por *scheduler_monitor_system_health_ring_buffer_recorded*.  
  
-   Errores en la asignación de CLR.  
  
-   Errores de conectividad mediante *connectivity_ring_buffer_recorded*.  
  
-   Errores de seguridad mediante *security_error_ring_buffer_recorded*.  

> [!NOTE]
> Para obtener más información sobre los interbloqueos, vea [Interbloqueos en la Guía de versiones de fila y bloqueo de transacciones](../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md#deadlocks).   
> Para obtener más información sobre los mensajes de error SQL, vea [Errores del motor de base de datos](../../relational-databases/errors-events/database-engine-events-and-errors.md).

## <a name="viewing-the-session-data"></a>Ver los datos de la sesión  
En la sesión se usa el destino del búfer en anillo y el del archivo de eventos para almacenar los datos. El destino de archivo de eventos está configurado con un tamaño máximo de 5 MB y una directiva de retención de archivo de cuatro archivos. 

Para ver los datos de sesión del destino del búfer en anillo con la interfaz de usuario de eventos extendidos disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vea [Visualización avanzada de datos de destino de eventos extendidos en SQL Server: Observar datos en directo](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md#b3-watch-live-data).

Para ver los datos de sesión del destino del búfer en anillo con [!INCLUDE[tsql](../../includes/tsql-md.md)], use la consulta siguiente:  
  
```sql  
SELECT CAST(xet.target_data as xml) 
FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
Para ver los datos de sesión del archivo de eventos, use la interfaz de usuario Eventos extendidos disponible en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, vea [Advanced Viewing of Target Data from Extended Events in SQL Server (Visualización avanzada de datos de destino de eventos extendidos en SQL Server)](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md).
  
## <a name="restoring-the-system_health-session"></a>Restaurar la sesión system_health  
Si elimina la sesión system_health, puede restaurarla si ejecuta el archivo **u_tables.sql** en el Editor de consultas. Este archivo se encuentra en la siguiente carpeta, donde **C:** representa la unidad en la que se han instalado los archivos de programa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y **MSSQL1x** la versión principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 `C:\Program Files\Microsoft SQL Server\MSSQL1x.\<*instanceid*>\MSSQL\Install`  
  
Tenga en cuenta que después de restaurar la sesión, debe iniciarla con la instrucción `ALTER EVENT SESSION` o mediante el nodo **Eventos extendidos** del Explorador de objetos. De lo contrario, la sesión se iniciará automáticamente la próxima vez que se reinicie el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)    
 [Herramientas de eventos extendidos](../../relational-databases/extended-events/extended-events-tools.md)    
 [Errores del motor de base de datos](../../relational-databases/errors-events/database-engine-events-and-errors.md)    
 [Vistas de catálogo de mensajes (para errores): sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 
