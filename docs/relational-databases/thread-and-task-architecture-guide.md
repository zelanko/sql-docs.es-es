---
title: "Guía de arquitectura de subprocesos y tareas | Microsoft Docs"
ms.custom: 
ms.date: 10/26/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: relational-databases-misc
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, thread and task architecture
- thread and task architecture guide
ms.assetid: 925b42e0-c5ea-4829-8ece-a53c6cddad3b
caps.latest.revision: 3
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 93be3a22ee517f90e65b8c8ba6dcaa8d90ed8515
ms.openlocfilehash: 3b835536b4f510021f0d966e3214cf1ec5f71f5c
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="thread-and-task-architecture-guide"></a>guía de arquitectura de subprocesos y tareas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Los subprocesos son una característica del sistema operativo que permite separar la lógica de aplicación en varias rutas de ejecución simultánea. Esta característica resulta útil cuando se trabaja con aplicaciones complejas que tienen muchas tareas que pueden ejecutarse a la vez. 

Cuando un sistema operativo ejecuta una instancia de una aplicación, crea una unidad llamada proceso para administrar la instancia. El proceso contiene un subproceso de ejecución. Se trata de una serie de instrucciones de programación que lleva a cabo el código de la aplicación. Por ejemplo, en una aplicación simple con un único conjunto de instrucciones que pueden ejecutarse en serie, solo hay una ruta de ejecución, o subproceso, en la aplicación. Las aplicaciones más complejas pueden tener varias tareas que podrían realizarse conjuntamente, no en serie. La aplicación puede hacerlo si inicia un proceso independiente para cada tarea. Sin embargo, iniciar un proceso es una operación que consume muchos recursos. En cambio, una aplicación puede iniciar subprocesos independientes. Se trata de elementos que consumen menos recursos. Además, cada subproceso puede programarse para ejecutarse independientemente de los demás subprocesos asociados a un proceso.

Los subprocesos permiten a las aplicaciones complejas hacer más eficaz el uso de una CPU, incluso en los equipos con una única CPU. Con una CPU solo puede ejecutarse un subproceso cada vez. Si un subproceso ejecuta una operación de larga duración que no utilice la CPU, como la lectura o la escritura en disco, otro de los subprocesos puede ejecutarse mientras termina la primera operación. La capacidad de ejecutar unos subprocesos mientras otros esperan a que una operación finalice permite a las aplicaciones maximizar su uso de la CPU. Esto es especialmente cierto para las aplicaciones multiusuario y las que realizan numerosas E/S de disco, como un servidor de base de datos. Los equipos con varios multiprocesadores o CPU pueden ejecutar un subproceso en cada CPU al mismo tiempo. Por ejemplo, si un equipo dispone de ocho CPU, podrá ejecutar ocho subprocesos simultáneamente.

## <a name="sql-server-batch-or-task-scheduling"></a>Programar tareas o lotes en SQL Server

### <a name="allocating-threads-to-a-cpu"></a>Asignar subprocesos a una CPU

De forma predeterminada, cada instancia de SQL Server inicia cada subproceso. Si se ha habilitado la afinidad, el sistema operativo asigna cada subproceso a una CPU concreta. El sistema operativo distribuye los subprocesos de las instancias de SQL Server entre los microprocesadores o las CPUs de un equipo según su carga. En ocasiones, también puede mover un subproceso de una CPU que se utiliza mucho a otra CPU. Por el contrario, el motor de base de datos de SQL Server asigna los subprocesos de trabajo a los programadores que distribuyen los subprocesos de manera uniforme entre las CPUs.

La opción de máscara de afinidad se establece utilizando [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md). Cuando no se establece la máscara de afinidad, la instancia de SQL Server asigna los subprocesos de trabajo de forma uniforme entre los programadores que no se han enmascarado.

### <a name="using-the-lightweight-pooling-option"></a>Usar la opción agrupación ligera

La sobrecarga que supone el cambio de contexto de los subprocesos no es excesiva. La mayoría de las instancias de SQL Server no registrarán diferencias de rendimiento entre la activación o desactivación de la agrupación ligera en 0 o 1. Las únicas instancias de SQL Server que podrían beneficiarse de la [agrupación ligera](../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) son las que se ejecutan en un equipo que tiene las características siguientes:    
* Un servidor de gran tamaño con varias CPU.
* Todas las CPU se ejecutan casi al máximo de su capacidad.
* Hay muchos cambios de contexto.

Estos sistemas pueden notar un pequeño incremento en el rendimiento si el valor de agrupación ligera se establece en 1.

No se recomienda utilizar la programación en modo de fibra para un funcionamiento habitual. La razón es que puede reducir el rendimiento al eliminar las ventajas normales del cambio de contexto, y que algunos componentes de SQL Server no funcionan correctamente en modo de fibra. Para obtener más información, vea lightweight pooling (opción de configuración del servidor).

## <a name="thread-and-fiber-execution"></a>Ejecución de subprocesos y fibras

Microsoft Windows utiliza un sistema de prioridad numérica con intervalos de 1 a 31 para programar subprocesos para su ejecución. El cero está reservado para el uso del sistema operativo. Cuando varios subprocesos esperan su ejecución, Windows genera el que tiene mayor prioridad.

De manera predeterminada, cada instancia de SQL Server tiene la prioridad 7, que se denomina prioridad normal. Esto proporciona a los subprocesos de SQL Server una prioridad lo suficientemente alta como para obtener los recursos adecuados de la CPU sin afectar negativamente a otras aplicaciones. 

La opción de configuración [aumento de prioridad](../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) se puede utilizar para aumentar la prioridad de los subprocesos de una instancia de SQL Server a 13. Se denomina prioridad alta. Esta configuración da a los subprocesos de SQL Server una prioridad más alta que la del resto de las aplicaciones. De esta forma, se tenderá a generar los subprocesos de SQL Server en cuanto estén listos para ejecutarse y no habrá subprocesos de otras aplicaciones con mayor prioridad. Esto puede mejorar el rendimiento cuando un servidor ejecuta únicamente instancias de SQL Server y ninguna otra aplicación. Sin embargo, si se produce en SQL Server una operación que consume mucha memoria, probablemente las demás aplicaciones no tendrán suficiente prioridad para tener preferencia ante el subproceso de SQL Server. 

Si está ejecutando varias instancias de SQL Server en un equipo y activa la opción aumento de prioridad solo para algunas instancias, se puede ver afectado el rendimiento de las instancias que se ejecutan con prioridad normal. También se puede ver afectado el rendimiento de otras aplicaciones y componentes del servidor si se activa aumento de prioridad. Por tanto, debe utilizarse bajo condiciones rigurosamente controladas.


## <a name="hot-add-cpu"></a>CPU instalada en caliente

Agregar CPU sin interrupción es la capacidad para agregar CPU de forma dinámica a un sistema en funcionamiento. Las CPU se pueden agregar físicamente, mediante la instalación de nuevo hardware; lógicamente, haciendo particiones de hardware en línea, o bien virtualmente a través de un nivel de virtualización. A partir de SQL Server 2008, SQL Server admite la característica de agregar CPU sin interrupción.

Requisitos para agregar CPU sin interrupción:  
* Se requiere hardware compatible con la función de agregar CPU sin interrupción.
* Se requiere la edición de 64 bits de Windows Server 2008 Datacenter o el sistema operativo Windows Server 2008 Enterprise Edition para sistemas basados en Itanium.
* Requiere SQL Server Enterprise.
* SQL Server no puede configurarse para el uso de NUMA de software. Para obtener más información sobre NUMA de software, consulte [Soft-NUMA (SQL Server)](../database-engine/configure-windows/soft-numa-sql-server.md).

SQL Server no empieza a utilizar automáticamente las CPUs una vez agregadas. Se evita así que SQL Server utilice CPUs que podrían haberse agregado con cualquier otro propósito. Una vez haya finalizado la agregación de CPUs, ejecute la instrucción [RECONFIGURE](../t-sql/language-elements/reconfigure-transact-sql.md) , a fin de que SQL Server reconozca las nuevas CPUs como recursos disponibles.

> [!NOTE]
> Si la [máscara affinity64](../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) estuviera configurada, es preciso modificarla para poder utilizar las nuevas CPUs.
 

## <a name="best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus"></a>Prácticas recomendadas para ejecutar SQL Server en equipos que tienen más de 64 CPU

### <a name="assigning-hardware-threads-with-cpus"></a>Asignar subprocesos de hardware a las CPU

No utilice las opciones de configuración del servidor Máscara de afinidad y Máscara de afinidad de 64 bits para enlazar procesadores a subprocesos específicos. Estas opciones están limitadas a 64 CPU. Utilice la opción SET PROCESS AFFINITY de [ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md) en su lugar.

### <a name="managing-the-transaction-log-file-size"></a>Administración del tamaño del archivo del registro de transacciones

El crecimiento automático no es un método fidedigno para aumentar el tamaño del archivo de registro de transacciones. El aumento del registro de transacciones debe ser un proceso en serie. La ampliación del registro puede hacer que las operaciones de escritura de transacciones no continúen hasta que finalice esta ampliación. En su lugar, asigne espacio previamente para los archivos de registro estableciendo el tamaño de archivo en un valor lo suficientemente alto para admitir la carga de trabajo habitual del entorno.

### <a name="setting-max-degree-of-parallelism-for-index-operations"></a>Configurar el grado máximo de paralelismo para las operaciones de índice

El rendimiento de las operaciones de índice como crear o volver a generar índices puede mejorarse en los equipos con muchas CPU estableciendo temporalmente el modelo de recuperación de la base de datos en el modelo de recuperación optimizado para cargas masivas de registros o en el modelo de recuperación simple. Estas operaciones de índice pueden generar actividad de registro significativa, y la contención del registro puede afectar a la elección del mejor grado de paralelismo (DOP) realizada por SQL Server.

Además, considere la posibilidad de ajustar la opción de configuración del servidor **Grado máximo de paralelismo (MAXDOP)** para estas operaciones. Las directrices siguientes se basan en pruebas internas y constituyen recomendaciones generales. Debe probar varios valores distintos para MAXDOP con objeto de determinar el valor óptimo para su entorno.

* Para el modelo de recuperación completa, limite el valor de la opción Grado máximo de paralelismo a ocho o menos.   
* Para el modelo para cargas masivas de registros o el modelo de recuperación simple, se debe tener en cuenta la posibilidad de establecer la opción Grado máximo de paralelismo en un valor superior a ocho.   
* Para los servidores con NUMA configurado, el grado máximo de paralelismo no debería superar el número de CPU asignadas a cada nodo NUMA. Esto se debe a que es más probable que la consulta utilice memoria local desde 1 nodo NUMA, lo que puede mejorar el tiempo de acceso a la memoria.  
* Para los servidores que tienen habilitada la tecnología Hyper-Threading y se fabricaron en 2009 o antes (antes de que se mejorara la característica Hyper-Threading), el valor MAXDOP no debería superar el número de procesadores físicos, en vez de procesadores lógicos.

Para obtener más información sobre la opción de grado máximo de paralelismo, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).

### <a name="setting-the-maximum-number-of-worker-threads"></a>Configurar el número máximo de subprocesos de trabajo

Establezca siempre el número máximo de subprocesos de trabajo en un valor superior al de la opción Grado máximo de paralelismo. El número de subprocesos de trabajo debe establecerse siempre en un valor de al menos siete veces el número de CPU del servidor. Para más información, consulte [Establecer la opción de configuración del servidor Máximo de subprocesos de trabajo](../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).

### <a name="using-sql-trace-and-sql-server-profiler"></a>Usar Seguimiento de SQL y SQL Server Profiler

 Se recomienda que no utilice Seguimiento de SQL y SQL Server Profiler en un entorno de producción. La sobrecarga para ejecutar estas herramientas también aumenta según lo hace el número de CPU. Si debe utilizar Seguimiento de SQL en un entorno de producción, reduzca al mínimo los eventos de seguimiento. Genere el perfil y pruebe de forma meticulosa cada evento de seguimiento sujeto a carga, y evite por otra parte utilizar combinaciones de eventos que afecten significativamente al rendimiento.

### <a name="setting-the-number-of-tempdb-data-files"></a>Establecer el número de archivos de datos tempdb

Normalmente, el número de archivos de datos tempdb debería coincidir con el número de CPUs. Sin embargo, si considera minuciosamente las necesidades de simultaneidad de tempdb, podrá simplificar la administración de la base de datos. Por ejemplo, si un sistema tiene 64 CPU y normalmente solo 32 consultas utilizan tempdb, al aumentar el número de archivos tempdb a 64 no se mejorará rendimiento.

### <a name="sql-server-components-that-can-use-more-than-64-cpus"></a>Componentes de SQL Server que pueden utilizar más de 64 CPU

La tabla siguiente contiene una lista de los componentes de SQL Server e indica si pueden utilizar más de 64 CPUs.

|Nombre del proceso   |Programa ejecutable |Utilizar más de 64 CPU |  
|----------|----------|----------|  
|Motor de base de datos de SQL Server |Sqlserver.exe  |Sí |  
|Reporting Services |Rs.exe |No |  
|Analysis Services  |As.exe |No |  
|Integration Services   |Is.exe |No |  
|Service Broker |Sb.exe |No |  
|Búsqueda de texto completo   |Fts.exe    |No |  
|Agente SQL Server   |Sqlagent.exe   |No |  
|SQL Server Management Studio   |Ssms.exe   |No |  
|programa de instalación de SQL Server   |Setup.exe  |No |  



