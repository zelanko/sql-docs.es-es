---
title: Guía de arquitectura de subprocesos y tareas | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
author: pmasl
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4c19e3ad3589cad6f7503ff9f0e92c090bef5035
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2020
ms.locfileid: "78340605"
---
# <a name="thread-and-task-architecture-guide"></a>guía de arquitectura de subprocesos y tareas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

## <a name="operating-system-task-scheduling"></a>Programación de tareas del sistema operativo
Los subprocesos son las unidades de procesamiento más pequeñas que puede ejecutar un sistema operativo y permiten que la lógica de la aplicación se separe en varias rutas de acceso de ejecución simultáneas. Los subprocesos son útiles cuando se trabaja con aplicaciones complejas que tienen muchas tareas que pueden ejecutarse a la vez. 

Cuando un sistema operativo ejecuta una instancia de una aplicación, crea una unidad llamada proceso para administrar la instancia. El proceso contiene un subproceso de ejecución. Se trata de una serie de instrucciones de programación que lleva a cabo el código de la aplicación. Por ejemplo, si una aplicación simple tiene un solo conjunto de instrucciones que se pueden ejecutar en serie, ese conjunto de instrucciones se administra como una **tarea** única y solo hay una ruta de ejecución (o **subproceso**) en la aplicación. Las aplicaciones más complejas pueden tener varias **tareas** que se podrían realizar de manera simultánea y no en serie. Para hacer esto, una aplicación puede iniciar procesos independientes para cada tarea, que es una operación que consume muchos recursos, o iniciar subprocesos independientes, que requieren menos recursos. Además, cada subproceso puede programarse para ejecutarse independientemente de los demás subprocesos asociados a un proceso.

Los subprocesos permiten a las aplicaciones complejas hacer más eficaz el uso de un procesador (CPU), incluso en los equipos con una única CPU. Con una CPU solo puede ejecutarse un subproceso cada vez. Si un subproceso ejecuta una operación de larga duración que no utilice la CPU, como la lectura o la escritura en disco, otro de los subprocesos puede ejecutarse mientras termina la primera operación. La capacidad de ejecutar unos subprocesos mientras otros esperan a que una operación finalice permite a las aplicaciones maximizar su uso de la CPU. Esto es especialmente cierto para las aplicaciones multiusuario y las que realizan numerosas E/S de disco, como un servidor de base de datos. Los equipos con varias CPU pueden ejecutar un subproceso en cada CPU al mismo tiempo. Por ejemplo, si un equipo dispone de ocho CPU, podrá ejecutar ocho subprocesos simultáneamente.

## <a name="sql-server-task-scheduling"></a>Programación de tareas de SQL Server
En el ámbito de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], una **solicitud** es la representación lógica de una consulta o lote. Una solicitud también representa las operaciones requeridas por los subprocesos del sistema, como el punto de control o el escritor de registros. Las solicitudes existen en varios estados a lo largo de su duración y pueden acumular esperas cuando no están disponibles los recursos necesarios para ejecutar la solicitud, como [bloqueos](../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md#locks) o [bloqueos temporales](../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md#latches). Para más información sobre los estados de la solicitud, consulte [sys.dm_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).

Una **tarea** representa la unidad de trabajo que se debe completar para satisfacer la solicitud. Se pueden asignar una o varias tareas a una solicitud única. Las solicitudes paralelas tendrán varias tareas activas que se ejecutan de manera simultánea y no en serie. Una solicitud que se ejecuta en serie solo tendrá una tarea activa en un momento dado. Las tareas existen en varios estados a lo largo de su duración. Para más información sobre los estados de la tarea, consulte [sys.dm_os_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md). Las tareas con un estado SUSPENDED están a la espera de que los recursos necesarios para ejecutar la tarea estén disponibles. Para más información sobre las tareas en espera, consulte [sys.dm_os_waiting_tasks](../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md).

Un **subproceso de trabajo** de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], también conocido como trabajo o subproceso, es una representación lógica de un subproceso de sistema operativo. Cuando se ejecutan solicitudes en serie, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] generará un trabajo para ejecutar la tarea activa. Cuando se ejecutan solicitudes en serie en [modo de fila](../relational-databases/query-processing-architecture-guide.md#execution-modes), [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] asigna un trabajo para coordinar los trabajos secundarios responsables de completar las tareas que tienen asignadas. El número de subprocesos de trabajo generados para cada tarea depende de:
-   Si la solicitud es válida para el paralelismo según lo determinado por el optimizador de consultas.
-   El [grado de paralelismo (DOP)](../relational-databases/query-processing-architecture-guide.md#DOP) disponible real en el sistema en función de la carga actual. Esto puede diferir del DOP estimado que está basado en la configuración del servidor para alcanzar el grado máximo de paralelismo (MAXDOP). Por ejemplo, la configuración de servidor para MAXDOP puede ser 8, pero el DOP disponible en tiempo de ejecución solo puede ser 2, lo que impacta en el rendimiento de la consulta. 

> [!NOTE]
> El límite del **grado máximo de paralelismo (MAXDOP)** se establece por tarea, no por solicitud. Esto significa que durante una ejecución de consulta en paralelo, una solicitud única puede generar varias tareas y cada tarea puede usar varios trabajos hasta alcanzar el límite MAXDOP. Para más información sobre MAXDOP, consulte [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

Un **programador**, conocido también como programador de SOS, administra los subprocesos de trabajo que requieren tiempo de procesamiento para hacer el trabajo en nombre de las tareas. Cada programador está asignado a un procesador individual (CPU). El tiempo que un trabajo puede permanecer activo en un programador se es el denominado cuanto del SO, con un máximo de 4 ms. Una vez que expira el tiempo de cuanto, un trabajo suspende su tiempo en favor de otros trabajos que necesitan acceder a los recursos de la CPU y cambia su estado. Esta cooperación entre los trabajos para maximizar el acceso a los recursos de la CPU se denomina **programación cooperativa**, también conocida como programación no preferente. A su vez, el cambio en el estado del trabajo se propaga a la tarea asociada con ese trabajo y a la solicitud asociada con la tarea. Para más información sobre los estados del trabajo, consulte [sys.dm_os_workers](../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md). Para más información sobre los programados, consulte [sys.dm_os_schedulers ](../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 

### <a name="allocating-threads-to-a-cpu"></a>Asignación de subprocesos a una CPU
De manera predeterminada, cada instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inicia cada subproceso, y el sistema operativo distribuye los subprocesos de las instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre los procesadores (las CPU) de un equipo en función de la carga. Si se ha habilitado la afinidad de proceso en el nivel de sistema operativo, el sistema operativo asigna cada subproceso a una CPU concreta. Por el contrario, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] asigna los **subprocesos de trabajo** de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a los **programadores** que distribuyen los subprocesos de manera uniforme entre las CPU.
    
Para llevar a cabo la multitarea, por ejemplo cuando varias aplicaciones acceden el mismo conjunto de CPU, en ocasiones el sistema operativo mueve los subprocesos de trabajo del entre diferentes CPU. Aunque esta actividad es eficaz desde el punto de vista del sistema operativo, puede reducir el rendimiento de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuando la carga del sistema es grande, ya que la memoria caché de cada procesador se carga repetidamente con datos. La asignación de CPU a subprocesos específicos puede mejorar el rendimiento en estas condiciones al eliminar las operaciones de repetición de carga del procesador y reducir la migración de subprocesos entre CPU (con lo que se reduce el cambio de contexto); dicha asociación entre un subproceso y un procesador se denomina afinidad del procesador. Si se ha habilitado la afinidad, el sistema operativo asigna cada subproceso a una CPU concreta. 

La [opción de máscara de afinidad](../database-engine/configure-windows/affinity-mask-server-configuration-option.md) se establece mediante [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md). Cuando no se establece la máscara de afinidad, la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asigna el máximo de subprocesos de trabajo de forma uniforme entre los programadores que no se han enmascarado.

> [!CAUTION]
> No configure la afinidad de CPU en el sistema operativo y la máscara de afinidad en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esta configuración intenta lograr el mismo resultado y, si las configuraciones no son coherentes, puede obtener resultados impredecibles. Para obtener más información, vea [affinity mask (opción de configuración del servidor)](../database-engine/configure-windows/affinity-mask-server-configuration-option.md).

La agrupación de subprocesos permite optimizar el rendimiento cuando un gran número de clientes se conecta al servidor. Normalmente, se crea un subproceso del sistema operativo independiente para cada solicitud de la consulta. Sin embargo, cuando hay cientos de conexiones al servidor, el uso de un subproceso por solicitud de consulta puede consumir grandes cantidades de recursos del sistema. La [opción Máximo de subprocesos de trabajo](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) permite que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cree un grupo de subprocesos de trabajo para atender un gran número de solicitudes de consulta, lo que mejora el rendimiento. 

### <a name="using-the-lightweight-pooling-option"></a>Usar la opción agrupación ligera
Es posible que la sobrecarga que supone el cambio de contexto de los subprocesos no sea excesiva. La mayoría de las instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no registrarán diferencias de rendimiento al establecer la opción de agrupación ligera en 0 o 1. Las únicas instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que podrían beneficiarse de la [agrupación ligera](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) son las que se ejecutan en un equipo que tiene las características siguientes:    
* Un servidor de gran tamaño con varias CPU.
* Todas las CPU se ejecutan casi al máximo de su capacidad.
* Hay un nivel elevado de cambios de contexto.

Estos sistemas pueden notar un pequeño incremento en el rendimiento si el valor de agrupación ligera se establece en 1.

> [!IMPORTANT]
> No use la programación en modo de fibra para un funcionamiento habitual. Esto puede reducir el rendimiento al impedir las ventajas normales del cambio de contexto, y que algunos componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no funcionen correctamente en el modo de fibra. Para obtener más información, vea [lightweight pooling (opción de configuración del servidor)](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).

## <a name="thread-and-fiber-execution"></a>Ejecución de subprocesos y fibras
Microsoft Windows utiliza un sistema de prioridad numérica con intervalos de 1 a 31 para programar subprocesos para su ejecución. El cero está reservado para el uso del sistema operativo. Cuando varios subprocesos esperan su ejecución, Windows genera el que tiene mayor prioridad.

De manera predeterminada, cada instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]tiene la prioridad 7, que se denomina prioridad normal. Esto proporciona a los subprocesos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] una prioridad lo suficientemente alta como para obtener los recursos adecuados de la CPU sin afectar negativamente a otras aplicaciones. 

La opción de configuración [Aumento de prioridad](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) se puede usar para aumentar la prioridad de los subprocesos de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a 13. Se denomina prioridad alta. Esta configuración da a los subprocesos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] una prioridad más alta que la del resto de las aplicaciones. De esta forma, se tenderá a generar los subprocesos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en cuanto estén listos para ejecutarse y no habrá subprocesos de otras aplicaciones con mayor prioridad. Esto puede mejorar el rendimiento cuando un servidor ejecuta únicamente instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y ninguna otra aplicación. Sin embargo, si se produce en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] una operación que consume mucha memoria, probablemente las demás aplicaciones no tendrán suficiente prioridad para tener preferencia ante el subproceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

Si está ejecutando varias instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un equipo y activa la opción aumento de prioridad solo para algunas instancias, se puede ver afectado el rendimiento de las instancias que se ejecutan con prioridad normal. También se puede ver afectado el rendimiento de otras aplicaciones y componentes del servidor si se activa aumento de prioridad. Por tanto, debe utilizarse bajo condiciones rigurosamente controladas.

## <a name="hot-add-cpu"></a>CPU instalada en caliente
Agregar CPU sin interrupción es la capacidad para agregar CPU de forma dinámica a un sistema en funcionamiento. Las CPU se pueden agregar físicamente, mediante la instalación de nuevo hardware; lógicamente, haciendo particiones de hardware en línea, o bien virtualmente a través de un nivel de virtualización. A partir de [!INCLUDE[ssKatmai](../includes/ssKatmai-md.md)], [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite la adición de CPU sin interrupción.

Requisitos para agregar CPU sin interrupción:  
* Se requiere hardware compatible con la función de agregar CPU sin interrupción.
* Se requiere la edición de 64 bits de Windows Server 2008 Datacenter o el sistema operativo Windows Server 2008 Enterprise Edition para sistemas basados en Itanium.
* Se requiere [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise.
* [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no puede configurarse para el uso de NUMA de software. Para obtener más información sobre NUMA de software, consulte [Soft-NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md).

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no empieza a utilizar automáticamente las CPUs una vez agregadas. Se evita así que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilice CPUs que podrían haberse agregado con cualquier otro propósito. Después de agregar las CPU, ejecute la instrucción [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md), para que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reconozca las nuevas CPU como recursos disponibles.

> [!NOTE]
> Si la [máscara affinity64](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) estuviera configurada, es preciso modificarla para poder utilizar las nuevas CPUs.
 
## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>Procedimientos recomendados para ejecutar SQL Server en equipos que tienen más de 64 CPU

### <a name="assigning-hardware-threads-with-cpus"></a>Asignar subprocesos de hardware a las CPU
No utilice las opciones de configuración del servidor Máscara de afinidad y Máscara de afinidad de 64 bits para enlazar procesadores a subprocesos específicos. Estas opciones están limitadas a 64 CPU. En su lugar, use la opción `SET PROCESS AFFINITY` de [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md).

### <a name="managing-the-transaction-log-file-size"></a>Administración del tamaño del archivo de registro de transacciones
El crecimiento automático no es un método fidedigno para aumentar el tamaño del archivo de registro de transacciones. El aumento del registro de transacciones debe ser un proceso en serie. La ampliación del registro puede hacer que las operaciones de escritura de transacciones no continúen hasta que finalice esta ampliación. En su lugar, asigne espacio previamente para los archivos de registro estableciendo el tamaño de archivo en un valor lo suficientemente alto para admitir la carga de trabajo habitual del entorno.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>Configuración del grado máximo de paralelismo para las operaciones de índice
El rendimiento de las operaciones de índice como crear o volver a generar índices puede mejorarse en los equipos con muchas CPU estableciendo temporalmente el modelo de recuperación de la base de datos en el modelo de recuperación optimizado para cargas masivas de registros o en el modelo de recuperación simple. Estas operaciones de índice pueden generar actividad de registro significativa, y la contención del registro puede afectar a la elección del mejor grado de paralelismo (DOP) realizada por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Además de ajustar la opción de configuración del servidor del **grado máximo de paralelismo (MAXDOP)** , considere ajustar el paralelismo para las operaciones de índice con la [opción MAXDOP](../t-sql/statements/alter-index-transact-sql.md). Para obtener más información, vea [Configurar operaciones de índice en paralelo](../relational-databases/indexes/configure-parallel-index-operations.md). Para más información e instrucciones sobre cómo ajustar la opción de configuración del servidor de grado máximo de paralelismo, consulte [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

### <a name="setting-the-maximum-number-of-worker-threads"></a>Configurar el número máximo de subprocesos de trabajo
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] configurará dinámicamente la opción de configuración del servidor **Número máximo de subprocesos de trabajo** en el inicio. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa el número de CPU disponibles y la arquitectura del sistema para determinar esta configuración de servidor durante el inicio, con una [fórmula](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md#Recommendations) documentada.

Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un profesional certificado de SQL Server. Si sospecha que hay un problema de rendimiento, probablemente no se deba a la disponibilidad de subprocesos de trabajo. La causa más probable es que haya alguna E/S que haga que los subprocesos de trabajo esperen. Lo mejor es buscar la causa principal de un problema de rendimiento antes de cambiar el valor de configuración de máximo de subprocesos de trabajo. Sin embargo, si necesita establecer manualmente el número máximo de subprocesos de trabajo, este valor de configuración siempre se debe establecer en un valor de al menos siete veces el número de CPU presentes en el sistema. Para más información, consulte [Configurar la opción de máximo de subprocesos de trabajo](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).

### <a name="using-sql-trace-and-sql-server-profiler"></a>Usar Seguimiento de SQL y SQL Server Profiler
No se recomienda usar Seguimiento de SQL y SQL Profiler en un entorno de producción. La sobrecarga para ejecutar estas herramientas también aumenta según lo hace el número de CPU. Si debe utilizar Seguimiento de SQL en un entorno de producción, reduzca al mínimo los eventos de seguimiento. Genere el perfil y pruebe de forma meticulosa cada evento de seguimiento sujeto a carga, y evite por otra parte utilizar combinaciones de eventos que afecten significativamente al rendimiento.

> [!IMPORTANT]
> Seguimiento de SQL y [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] están en desuso. El espacio de nombres *Microsoft.SqlServer.Management.Trace* que contiene los objetos Trace y Replay de Microsoft SQL Server también están en desuso. 
> [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] 
> Use eventos extendidos en su lugar. Para más información sobre los [eventos extendidos](../relational-databases/extended-events/extended-events.md), vea [Inicio rápido: Eventos extendidos en SQL Server](../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md) y [Generador de perfiles XEvent de SSMS](../relational-databases/extended-events/use-the-ssms-xe-profiler.md).

> [!NOTE]
> [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] para las cargas de trabajo de Analysis Services NO está en desuso y seguirá siendo compatible.

### <a name="setting-the-number-of-tempdb-data-files"></a>Establecer el número de archivos de datos TempDB
El número de archivos depende del número de procesadores (lógicos) de la máquina. Como regla general, si el número de procesadores lógicos es inferior o igual a ocho, use el mismo número de archivos de datos que procesadores lógicos. Si el número de procesadores lógicos es superior a ocho, use ocho archivos de datos y, después, si se mantiene la contención, aumente el número de archivos de datos en múltiplos de 4 hasta que la contención se reduzca a niveles aceptables, o bien modifique el código o la carga de trabajo. Tenga en cuenta también otras recomendaciones para TempDB, disponibles en [Optimizar el rendimiento de TempDB en SQL Server](../relational-databases/databases/tempdb-database.md#optimizing-tempdb-performance-in-sql-server). 

Sin embargo, si considera minuciosamente las necesidades de simultaneidad de tempdb, podrá simplificar la carga administrativa de la base de datos. Por ejemplo, si un sistema tiene 64 CPU y normalmente solo 32 consultas utilizan tempdb, al aumentar el número de archivos tempdb a 64 no se mejorará rendimiento.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>Componentes de SQL Server que pueden utilizar más de 64 CPU
En la tabla siguiente se enumeran los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y se indica si pueden usar más de 64 CPU.

|Nombre del proceso   |Programa ejecutable |Utilizar más de 64 CPU |  
|----------|----------|----------|  
|Motor de base de datos de SQL Server |Sqlserver.exe  |Sí |  
|Reporting Services |Rs.exe |Sin |  
|Analysis Services  |As.exe |Sin |  
|Integration Services   |Is.exe |Sin |  
|Service Broker |Sb.exe |Sin |  
|Búsqueda de texto completo   |Fts.exe    |Sin |  
|Agente SQL Server   |Sqlagent.exe   |Sin |  
|SQL Server Management Studio   |Ssms.exe   |Sin |  
|programa de instalación de SQL Server   |Setup.exe  |Sin |  
