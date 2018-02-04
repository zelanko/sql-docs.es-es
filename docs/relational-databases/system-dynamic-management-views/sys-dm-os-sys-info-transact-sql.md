---
title: sys.dm_os_sys_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_os_sys_info_TSQL
- dm_os_sys_info
- dm_os_sys_info_TSQL
- sys.dm_os_sys_info
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_sys_info dynamic management view
- time [SQL Server], instance started
- starting time
ms.assetid: 20f6bc9c-839a-4fa4-b3f3-a6c47d1b69af
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 21fe61d34a9b8823af499b64aef0eaef95c1a92e
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmossysinfo-transact-sql"></a>sys.dm_os_sys_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Devuelve diversos datos útiles sobre el equipo y los recursos disponibles y consumidos por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
> **Nota:** para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_sys_info**.  
  
|Nombre de columna|Tipo de datos|Descripción y notas de la versión específica |  
|-----------------|---------------|-----------------|  
|**cpu_ticks**|**bigint**|Especifica el contador actual de CPU. Los tics de CPU se obtienen del contador de RDTSC del procesador. Es un número que aumenta regularmente. No acepta valores NULL.|  
|**ms_ticks**|**bigint**|Especifica el número de milisegundos transcurridos desde que se inició el equipo. No acepta valores NULL.|  
|**cpu_count**|**int**|Especifica el número de CPUs lógicas en el sistema. No acepta valores NULL.|  
|**hyperthread_ratio**|**int**|Especifica la proporción del número de núcleos lógicos o físicos expuestos por un paquete de procesadores físicos. No acepta valores NULL.|  
|**physical_memory_in_bytes**|**bigint**|**Se aplica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Especifica la cantidad total de memoria física en el equipo. No acepta valores NULL.|  
|**physical_memory_kb**|**bigint**|**Se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Especifica la cantidad total de memoria física en el equipo. No acepta valores NULL.|  
|**virtual_memory_in_bytes**|**bigint**|**Se aplica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Cantidad de memoria virtual disponible para el proceso en modo usuario. Se puede utilizar para determinar si SQL Server se inició utilizando un modificador 3-GB.|  
|**virtual_memory_kb**|**bigint**|**Se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Especifica la cantidad total de espacio de direcciones virtuales disponible para el proceso en modo usuario. No acepta valores NULL.|  
|**bpool_commited**|**int**|**Se aplica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Representa la memoria confirmada en kilobytes (KB) en el administrador de memoria. No incluye la memoria reservada del administrador de memoria. No acepta valores NULL.|  
|**committed_kb**|**int**|**Se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Representa la memoria confirmada en kilobytes (KB) en el administrador de memoria. No incluye la memoria reservada del administrador de memoria. No acepta valores NULL.|  
|**bpool_commit_target**|**int**|**Se aplica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Representa la cantidad de memoria, en kilobytes (KB), que el administrador de memoria de SQL Server puede utilizar.|  
|**committed_target_kb**|**int**|**Se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Representa la cantidad de memoria, en kilobytes (KB), que el administrador de memoria de SQL Server puede utilizar. La cantidad de destino se calcula utilizando una serie de entradas como las siguientes:<br /><br /> -el estado actual del sistema, incluida su carga<br /><br /> -la memoria solicitada por los procesos actuales<br /><br /> -la cantidad de memoria instalada en el equipo<br /><br /> -parámetros de configuración<br /><br /> Si **committed_target_kb** es mayor que **committed_kb**, el Administrador de memoria intentará obtener memoria adicional. Si **committed_target_kb** es menor que **committed_kb**, el Administrador de memoria intentará reducir la cantidad de memoria asignada. El **committed_target_kb** siempre incluye memoria descartada y la reservada. No acepta valores NULL.|  
|**bpool_visible**|**int**|**Se aplica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]** .<br /><br /> Número de búferes de 8 KB del grupo de búferes accesibles directamente en el espacio de direcciones virtuales de proceso. Cuando no se utilizan las Extensiones de ventana de dirección (AWE), si el grupo de búferes ha obtenido el destino de memoria (bpool_committed = bpool_commit_target), el valor de bpool_visible es igual al valor de bpool_committed. Si se utiliza AWE en una versión de 32 bits de SQL Server, bpool_visible representa el tamaño de la ventana de la asignación AWE utilizada para tener acceso a la memoria física asignada por el grupo de búferes. El tamaño de esta ventana de asignación está limitado por el espacio de direcciones de proceso y, por tanto, la cantidad visible será inferior a la asignada, y puede verse reducida aún más por componentes internos que consumen memoria para propósitos no relacionados con las páginas de base de datos. Si el valor de bpool_visible es demasiado bajo, es posible que se produzcan errores de memoria insuficiente.|  
|**visible_target_kb**|**int**|**Se aplica a: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Es el mismo que **committed_target_kb**. No acepta valores NULL.|  
|**stack_size_in_bytes**|**int**|Especifica el tamaño de la pila de llamadas de cada subproceso creado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**os_quantum**|**bigint**|Representa el cuanto de una tarea no preferente medido en milisegundos. Cuanto (en segundos) = **os_quantum** / velocidad de reloj de CPU. No acepta valores NULL.|  
|**os_error_mode**|**int**|Especifica el modo de error para el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**os_priority_class**|**int**|Especifica la clase de prioridad del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Acepta valores NULL.<br /><br /> 32 = Normal (el registro de errores indicará que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está iniciando con una prioridad base normal (=7)).<br /><br /> 128 = Alto (el registro de errores indicará que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando con una prioridad base alta.  (=13).)<br /><br /> Para más información, consulte [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).|  
|**max_workers_count**|**int**|Representa el número máximo de subprocesos de trabajo que se pueden crear. No acepta valores NULL.|  
|**scheduler_count**|**int**|Representa el número de programadores de usuario configurados en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**scheduler_total_count**|**int**|Representa el número total de programadores en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No acepta valores NULL.|  
|**deadlock_monitor_serial_number**|**int**|Especifica el identificador de la secuencia del monitor de interbloqueos actual. No acepta valores NULL.|  
|**sqlserver_start_time_ms_ticks**|**bigint**|Representa la **ms_tick** número cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inició por última vez. Comparar a la columna actual ms_ticks. No acepta valores NULL.|  
|**sqlserver_start_time**|**datetime**|Especifica la fecha y la hora en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inició por última vez. No acepta valores NULL.|  
|**affinity_type**|**int**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**  a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica el tipo de la afinidad de proceso de la CPU de servidor actualmente en uso. No acepta valores NULL. Para obtener más información, vea [ALTER SERVER CONFIGURATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-configuration-transact-sql.md).<br /><br /> 1 = MANUAL<br /><br /> 2 = AUTO|  
|**affinity_type_desc**|**varchar(60)**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Describe la **affinity_type** columna. No acepta valores NULL.<br /><br /> MANUAL = la afinidad se ha establecido para al menos una CPU.<br /><br /> AUTO = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede mover libremente los subprocesos entre las CPU.|  
|**process_kernel_time_ms**|**bigint**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [! INCLUDE [ssCurrent]**(.. /Token/ssCurrent_md.MD)].<br /><br /> Tiempo total en milisegundos que han tardado todos los subprocesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo kernel. Este valor puede ser mayor que el de un único reloj de procesador porque incluye el tiempo para todos los procesadores del servidor. No acepta valores NULL.|  
|**process_user_time_ms**|**bigint**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Tiempo total en milisegundos que han tardado todos los subprocesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo usuario. Este valor puede ser mayor que el de un único reloj de procesador porque incluye el tiempo para todos los procesadores del servidor. No acepta valores NULL.|  
|**time_source**|**int**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Indica la API que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza para recuperar el tiempo de reloj. No acepta valores NULL.<br /><br /> 0 = QUERY_PERFORMANCE_COUNTER<br /><br /> 1 = MULTIMEDIA_TIMER|  
|**time_source_desc**|**nvarchar(60)**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Describe la **time_source** columna. No acepta valores NULL.<br /><br /> QUERY_PERFORMANCE_COUNTER = el [QueryPerformanceCounter](http://go.microsoft.com/fwlink/?LinkId=163095) API recupera la hora de reloj.<br /><br /> MULTIMEDIA_TIMER = el [temporizador multimedia](http://go.microsoft.com/fwlink/?LinkId=163094) API que recupera la hora de reloj.|  
|**virtual_machine_type**|**int**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Indica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un entorno virtualizado.  No acepta valores NULL.<br /><br /> 0 = NONE<br /><br /> 1 = HYPERVISOR<br /><br /> 2 = OTHER|  
|**virtual_machine_type_desc**|**nvarchar(60)**|**Se aplica a: [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Describe la **virtual_machine_type** columna. No acepta valores NULL.<br /><br /> NONE = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando en una máquina virtual.<br /><br /> HYPERVISOR = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando en un hipervisor, lo que implica una virtualización asistida por hardware. Cuando se instala el rol Hyper_V, el hipervisor hospeda el sistema operativo, por lo que una instancia en ejecución en el sistema operativo del host se ejecuta en el hipervisor.<br /><br /> OTHER = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando en una máquina virtual que no emplea asistencia por hardware, por ejemplo Microsoft Virtual PC.|  
|**softnuma_configuration**|**int**|**Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> Especifica que se configuran los nodos NUMA de forma. No acepta valores NULL.<br /><br /> 0 = OFF indica el valor predeterminado de hardware<br /><br /> 1 = NUMA de software automática<br /><br /> 2 = soft-NUMA manual a través del registro|  
|**softnuma_configuration_desc**|**nvarchar(60)**|**Se aplica a: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** .<br /><br /> OFF = Soft-NUMA característica está desactivada<br /><br /> ON = SQL Server automáticamente determina los tamaños de nodo NUMA para NUMA de software<br /><br /> MANUAL = soft-NUMA configurado manualmente|
|**process_physical_affinity**|**nvarchar(3072)** |**Se aplica a: a partir de [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]** .<br /><br />Información aún se proporcionará. |
|**sql_memory_model**|**int**|**Se aplica a: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 a partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Especifica el modelo de memoria utilizado por SQL Server para asignar memoria. No acepta valores NULL.<br /><br />1 = modelo de memoria convencional<br />2 = bloquear páginas en memoria<br /> 3 = páginas grandes en la memoria|
|**sql_memory_model_desc**|**nvarchar(120)**|**Se aplica a: [!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 a partir [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1**.<br /><br />Especifica el modelo de memoria utilizado por SQL Server para asignar memoria. No acepta valores NULL.<br /><br />**CONVENCIONAL** = SQL Server está usando el modelo de memoria convencional para asignar memoria. Este es el modelo de memoria de sql de predeterminado cuando la cuenta de servicio de SQL Server no tiene bloquear páginas en los privilegios de memoria durante el inicio.<br />**LOCK_PAGES** = SQL server está usando bloquear páginas en memoria para asignar memoria. Este es el Administrador de memoria de sql de forma predeterminada cuando la cuenta de servicio de SQL Server poseer bloquear páginas en el privilegio de memoria durante el inicio de SQL Server.<br /> **LARGE_PAGES** = SQL Server está utilizando páginas grandes en la memoria para asignar memoria. SQL Server utiliza el asignador de páginas grandes para asignar memoria sólo con Enterprise edition cuando la cuenta de servicio de SQL Server poseer bloquear páginas en privilegios de memoria durante el inicio del servidor y cuando está activado 834 de marca de seguimiento.|
|**pdw_node_id**|**int**|**Se aplica a: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]**<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
|**socket_count** |**int** | **Se aplica a: a partir de [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]** .<br /><br />Especifica el número de sockets de procesador disponibles en el sistema. |  
|**cores_per_socket** |**int** | **Se aplica a: a partir de [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Especifica el número de procesadores por socket disponible en el sistema. |  
|**numa_node_count** |**int** | **Se aplica a: a partir de [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].**.<br /><br />Especifica el número de nodos numa disponibles en el sistema. Esta columna incluye nodos numa físicos, así como nodos numa de software. |  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere `VIEW SERVER STATE` permiso en el servidor.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles Premium requieren el `VIEW DATABASE STATE` permiso en la base de datos. En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] niveles estándar y básico requiere la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] cuenta de administrador.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operativo SQL Server relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  



