---
title: Guía de arquitectura de subprocesos y tareas | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
author: rothja
ms.author: jroth
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2d0c25e433fd9e311908d1759bbe75a1e1a1f045
ms.sourcegitcommit: 7e828cd92749899f4e1e45ef858ceb9a88ba4b6a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51629596"
---
# <a name="thread-and-task-architecture-guide"></a>guía de arquitectura de subprocesos y tareas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Los subprocesos son una característica del sistema operativo que permite separar la lógica de aplicación en varias rutas de ejecución simultánea. Esta característica resulta útil cuando se trabaja con aplicaciones complejas que tienen muchas tareas que pueden ejecutarse a la vez. 

Cuando un sistema operativo ejecuta una instancia de una aplicación, crea una unidad llamada proceso para administrar la instancia. El proceso contiene un subproceso de ejecución. Se trata de una serie de instrucciones de programación que lleva a cabo el código de la aplicación. Por ejemplo, en una aplicación simple con un único conjunto de instrucciones que pueden ejecutarse en serie, solo hay una ruta de ejecución, o subproceso, en la aplicación. Las aplicaciones más complejas pueden tener varias tareas que podrían realizarse conjuntamente, no en serie. La aplicación puede hacerlo si inicia un proceso independiente para cada tarea. Sin embargo, iniciar un proceso es una operación que consume muchos recursos. En cambio, una aplicación puede iniciar subprocesos independientes. Se trata de elementos que consumen menos recursos. Además, cada subproceso puede programarse para ejecutarse independientemente de los demás subprocesos asociados a un proceso.

Los subprocesos permiten a las aplicaciones complejas hacer más eficaz el uso de una CPU, incluso en los equipos con una única CPU. Con una CPU solo puede ejecutarse un subproceso cada vez. Si un subproceso ejecuta una operación de larga duración que no utilice la CPU, como la lectura o la escritura en disco, otro de los subprocesos puede ejecutarse mientras termina la primera operación. La capacidad de ejecutar unos subprocesos mientras otros esperan a que una operación finalice permite a las aplicaciones maximizar su uso de la CPU. Esto es especialmente cierto para las aplicaciones multiusuario y las que realizan numerosas E/S de disco, como un servidor de base de datos. Los equipos con varios multiprocesadores o CPU pueden ejecutar un subproceso en cada CPU al mismo tiempo. Por ejemplo, si un equipo dispone de ocho CPU, podrá ejecutar ocho subprocesos simultáneamente.

## <a name="sql-server-batch-or-task-scheduling"></a>Programar tareas o lotes en SQL Server

### <a name="allocating-threads-to-a-cpu"></a>Asignar subprocesos a una CPU
De forma predeterminada, cada instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inicia cada subproceso, y el sistema operativo distribuye los subprocesos de las instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] entre las CPU de un equipo en función de la carga. Si se ha habilitado la afinidad de proceso en el nivel de sistema operativo, el sistema operativo asigna cada subproceso a una CPU concreta. Por el contrario, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] asigna subprocesos de trabajo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a los programadores que distribuyen los subprocesos de manera uniforme entre los procesadores (CPU).
    
Para llevar a cabo la multitarea, por ejemplo cuando varias aplicaciones acceden el mismo conjunto de procesadores, en ocasiones el sistema operativo mueve los subprocesos del proceso entre diferentes procesadores. Aunque esta actividad es eficaz desde el punto de vista del sistema operativo, puede reducir el rendimiento de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuando la carga del sistema es grande, ya que la memoria caché de cada procesador se carga repetidamente con datos. La asignación de procesadores a subprocesos específicos puede mejorar el rendimiento en estas condiciones al eliminar las operaciones de repetición de carga del procesador y reducir la migración de subprocesos entre procesadores (con lo que se reduce el cambio de contexto); dicha asociación entre un subproceso y un procesador se denomina afinidad del procesador. Si se ha habilitado la afinidad, el sistema operativo asigna cada subproceso a una CPU concreta. 

La [opción de máscara de afinidad](../database-engine/configure-windows/affinity-mask-server-configuration-option.md) se establece mediante [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md). Cuando no se establece la máscara de afinidad, la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asigna el máximo de subprocesos de trabajo de forma uniforme entre los programadores que no se han enmascarado.

> [!CAUTION]
> No configure la afinidad de CPU en el sistema operativo y la máscara de afinidad en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Esta configuración intenta lograr el mismo resultado y, si las configuraciones no son coherentes, puede obtener resultados impredecibles. Para obtener más información, vea [affinity mask (opción de configuración del servidor)](../database-engine/configure-windows/affinity-mask-server-configuration-option.md).

La agrupación de subprocesos permite optimizar el rendimiento cuando un gran número de clientes se conecta al servidor. Normalmente, se crea un subproceso del sistema operativo independiente para cada solicitud de la consulta. Sin embargo, cuando hay cientos de conexiones al servidor, el uso de un subproceso por solicitud de consulta puede consumir grandes cantidades de recursos del sistema. La [opción Máximo de subprocesos de trabajo](..//database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) permite que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cree un grupo de subprocesos de trabajo para atender un gran número de solicitudes de consulta, lo que mejora el rendimiento. 

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
 
## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>Prácticas recomendadas para ejecutar SQL Server en equipos que tienen más de 64 CPU

### <a name="assigning-hardware-threads-with-cpus"></a>Asignar subprocesos de hardware a las CPU
No utilice las opciones de configuración del servidor Máscara de afinidad y Máscara de afinidad de 64 bits para enlazar procesadores a subprocesos específicos. Estas opciones están limitadas a 64 CPU. Utilice la opción SET PROCESS AFFINITY de [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) en su lugar.

### <a name="managing-the-transaction-log-file-size"></a>Administración del tamaño del archivo del registro de transacciones
El crecimiento automático no es un método fidedigno para aumentar el tamaño del archivo de registro de transacciones. El aumento del registro de transacciones debe ser un proceso en serie. La ampliación del registro puede hacer que las operaciones de escritura de transacciones no continúen hasta que finalice esta ampliación. En su lugar, asigne espacio previamente para los archivos de registro estableciendo el tamaño de archivo en un valor lo suficientemente alto para admitir la carga de trabajo habitual del entorno.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>Configurar el grado máximo de paralelismo para las operaciones de índice
El rendimiento de las operaciones de índice como crear o volver a generar índices puede mejorarse en los equipos con muchas CPU estableciendo temporalmente el modelo de recuperación de la base de datos en el modelo de recuperación optimizado para cargas masivas de registros o en el modelo de recuperación simple. Estas operaciones de índice pueden generar actividad de registro significativa, y la contención del registro puede afectar a la elección del mejor grado de paralelismo (DOP) realizada por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

Además, considere la posibilidad de ajustar la opción de configuración del servidor **Grado máximo de paralelismo (MAXDOP)** para estas operaciones. Las directrices siguientes se basan en pruebas internas y constituyen recomendaciones generales. Debe probar varios valores distintos para MAXDOP con objeto de determinar el valor óptimo para su entorno.

* Para el modelo de recuperación completa, limite el valor de la opción Grado máximo de paralelismo a ocho o menos.   
* Para el modelo para cargas masivas de registros o el modelo de recuperación simple, se debe tener en cuenta la posibilidad de establecer la opción Grado máximo de paralelismo en un valor superior a ocho.   
* Para los servidores con NUMA configurado, el grado máximo de paralelismo no debería superar el número de CPU asignadas a cada nodo NUMA. Esto se debe a que es más probable que la consulta utilice memoria local desde 1 nodo NUMA, lo que puede mejorar el tiempo de acceso a la memoria.  
* Para los servidores que tienen habilitada la tecnología Hyper-Threading y se fabricaron en 2009 o antes (antes de que se mejorara la característica Hyper-Threading), el valor MAXDOP no debería superar el número de procesadores físicos, en vez de procesadores lógicos.

Para obtener más información sobre la opción de grado máximo de paralelismo, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

### <a name="setting-the-maximum-number-of-worker-threads"></a>Configurar el número máximo de subprocesos de trabajo
Establezca siempre el número máximo de subprocesos de trabajo en un valor superior al de la opción Grado máximo de paralelismo. El número de subprocesos de trabajo debe establecerse siempre en un valor de al menos siete veces el número de CPU del servidor. Para más información, consulte [Establecer la opción de configuración del servidor Máximo de subprocesos de trabajo](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).

### <a name="using-sql-trace-and-sql-server-profiler"></a>Usar Seguimiento de SQL y SQL Server Profiler
No se recomienda usar Seguimiento de SQL y SQL Profiler en un entorno de producción. La sobrecarga para ejecutar estas herramientas también aumenta según lo hace el número de CPU. Si debe utilizar Seguimiento de SQL en un entorno de producción, reduzca al mínimo los eventos de seguimiento. Genere el perfil y pruebe de forma meticulosa cada evento de seguimiento sujeto a carga, y evite por otra parte utilizar combinaciones de eventos que afecten significativamente al rendimiento.

### <a name="setting-the-number-of-tempdb-data-files"></a>Establecer el número de archivos de datos tempdb
Normalmente, el número de archivos de datos tempdb debería coincidir con el número de CPUs. Sin embargo, si considera minuciosamente las necesidades de simultaneidad de tempdb, podrá simplificar la administración de la base de datos. Por ejemplo, si un sistema tiene 64 CPU y normalmente solo 32 consultas utilizan tempdb, al aumentar el número de archivos tempdb a 64 no se mejorará rendimiento.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>Componentes de SQL Server que pueden utilizar más de 64 CPU
En la tabla siguiente se enumeran los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y se indica si pueden usar más de 64 CPU.

|Nombre del proceso   |Programa ejecutable |Utilizar más de 64 CPU |  
|----------|----------|----------|  
|Motor de base de datos de SQL Server |Sqlserver.exe  |Sí |  
|Reporting Services |Rs.exe |no |  
|Analysis Services  |As.exe |no |  
|Integration Services   |Is.exe |no |  
|Service Broker |Sb.exe |no |  
|Búsqueda de texto completo   |Fts.exe    |no |  
|Agente SQL Server   |Sqlagent.exe   |no |  
|SQL Server Management Studio   |Ssms.exe   |no |  
|programa de instalación de SQL Server   |Setup.exe  |no |  
