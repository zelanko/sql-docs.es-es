---
title: "Guía de arquitectura de administración de memoria | Microsoft Docs"
ms.custom: 
ms.date: 10/21/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- guide, memory management architecture
- memory management architecture guide
ms.assetid: 7b0d0988-a3d8-4c25-a276-c1bdba80d6d5
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d00e5c97e6c27f3fe40b2066b5e194b8011f6b1e
ms.lasthandoff: 04/11/2017

---
# <a name="memory-management-architecture-guide"></a>guía de arquitectura de administración de memoria
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

## <a name="memory-architecture"></a>Arquitectura de la memoria

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquiere y libera memoria de manera dinámica según sea preciso. Normalmente, no es necesario que un administrador especifique la cantidad de memoria que se debe asignar a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], aunque todavía existe esta opción y es necesaria en algunos entornos.

Uno de los principales objetivos de diseño de todo el software de base de datos es minimizar la E/S de disco porque las operaciones de lectura y escritura del disco realizan un uso muy intensivo de los recursos. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] crea un grupo de búferes en la memoria para contener las páginas leídas en la base de datos. Gran parte del código de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está dedicado a minimizar el número de lecturas y escrituras físicas entre el disco y el grupo de búferes. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] intenta encontrar un equilibrio entre dos objetivos:

* Evitar que el grupo de búferes sea tan grande que todo el sistema se quede con poca memoria.
* Minimizar la E/S física a los archivos de base de datos al maximizar el tamaño del grupo de búferes.


> [!NOTE]
> En un sistema con mucha carga, algunas consultas grandes que necesitan una gran cantidad de memoria para ejecutarse no pueden obtener la cantidad mínima de memoria solicitada y reciben un error de tiempo de espera agotado mientras esperan los recursos de memoria. Para solucionarlo, aumente la [opción Espera de consulta](../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md). Para una consulta en paralelo, considere la posibilidad de reducir la [opción Grado máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
 
> [!NOTE]
> En un sistema con mucha carga y mucha presión de la memoria, las consultas con combinaciones de mezcla, orden y mapa de bits en el plan de consulta pueden quitar el mapa de bits si no obtienen la memoria mínima necesaria para dicho mapa de bits. Esto puede afectar al rendimiento de la consulta y, si el proceso de ordenación no cabe en la memoria, puede aumentar el uso de las tablas de trabajo en la base de datos tempdb, lo que hace que tempdb crezca. Para resolver este problema, agregue memoria física u optimice las consultas para que usen otro plan de consulta más rápido.
 
### <a name="providing-the-maximum-amount-of-memory-to-includessnoversionincludesssnoversion-mdmd"></a>Proporcionar la cantidad máxima de memoria a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

Mediante AWE y el privilegio Bloquear páginas en memoria, puede proporcionar las siguientes cantidades de memoria al Motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . (En la siguiente tabla se incluye una columna para las versiones de 32 bits que ya no están disponibles).

| |32 bits <sup>1</sup> |64 bits
|-------|-------|-------| 
|Memoria convencional |Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Hasta el límite de espacio de direcciones virtuales del proceso: <br>- 2 GB<br>- 3 GB con el parámetro de arranque /3gb <sup>2</sup> <br>- 4 GB en WOW64 <sup>3</sup> |Todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Hasta el límite de espacio de direcciones virtuales del proceso: <br>- 7 TB con la arquitectura IA64 (IA64 no se admite en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y versiones superiores)<br>- Sistema operativo máximo con arquitectura x64 <sup>4</sup>
|Mecanismo AWE (permite a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] superar el límite del espacio de direcciones virtuales del proceso en plataformas de 32 bits). |Ediciones Standard, Enterprise y Developer de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : el grupo de búferes puede tener acceso a un máximo de 64 GB de memoria.|No aplicable <sup>5</sup> |
|Privilegio del sistema operativo (OS) Bloquear páginas en la memoria (permite bloquear memoria física e impedir la paginación en el sistema operativo de la memoria bloqueada). <sup>6</sup> |Ediciones Standard, Enterprise y Developer de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]: requerido para que el proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilice el mecanismo AWE. La memoria asignada a través del mecanismo AWE no se puede paginar. <br> Si se concede este privilegio sin habilitar AWE, no tiene efecto en el servidor. |Ediciones Enterprise y Developer de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : recomendado para evitar la paginación del sistema operativo. Puede proporcionar una ventaja de rendimiento en función de la carga de trabajo. La cantidad de memoria a la que se puede tener acceso es similar al caso de memoria convencional. |

<sup>1</sup> Las versiones de 32 bits no están disponibles a partir de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
<sup>2</sup> /3gb es un parámetro de arranque del sistema operativo. Para obtener más información, visite MSDN Library.  
<sup>3</sup> WOW64 (Windows on Windows 64) es un modo en el que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de 32 bits se ejecuta en un sistema operativo de 64 bits.  
<sup>4</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition supports up to 128 GB. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition admite el máximo del sistema operativo máximo.  
<sup>5</sup> Tenga en cuenta que la opción sp_configure awe enabled estaba presente en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]de 64 bits, pero se omite.    
<sup>6</sup> Si se concede el privilegio Bloquear páginas en la memoria (LPIM) (con compatibilidad de 32 bits para AWE o directamente en 64 bits), se recomienda establecer también la opción Memoria de servidor máxima.

> [!NOTE]
> Las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pueden ejecutarse en un sistema operativo de 32 bits. Para acceder a más de 4 gigabytes de memoria en un sistema operativo de 32 bits, se requieren las extensiones de ventana de dirección (AWE) para administrar la memoria. Esto no es necesario cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ejecuta en sistemas operativos de 64 bits. Para más información acerca de AWE, consulte [Espacio de dirección del proceso](https://msdn.microsoft.com/library/ms189334) y [Administrar la memoria para bases de datos de gran tamaño](https://msdn.microsoft.com/library/ms191481) en la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2008.   


## <a name="dynamic-memory-management"></a>Administración dinámica de memoria

El comportamiento predeterminado de administración de memoria del motor de base de datos de Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es adquirir toda la memoria que necesita sin provocar una escasez de memoria en el sistema. El motor de base de datos lo consigue mediante las API de notificación de memoria de Microsoft Windows.

El espacio de dirección virtual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se puede dividir en dos regiones diferenciadas: espacio ocupado por el grupo de búferes y el resto. Si el mecanismo AWE está habilitado, el grupo de búferes puede residir en la memoria asignada de AWE, lo que proporciona espacio adicional para las páginas de base de datos. 

El grupo de búferes se utiliza como origen principal de asignación de memoria de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Los componentes externos que residen dentro del proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como los objetos COM, y que no reconocen los recursos de administración de memoria de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , usan la memoria situada fuera del espacio de direcciones virtuales ocupado por el grupo de búferes.

Cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se inicia, calcula el tamaño del espacio de direcciones virtuales del grupo de búferes basándose en un número de parámetros, como  la cantidad de memoria física en el sistema, el número de subprocesos de servidor y varios parámetros de inicio. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserva la cantidad calculada de su espacio de direcciones virtuales del proceso para el grupo de búferes, pero solo adquiere (confirma) la cantidad necesaria de memoria física para la carga actual.

A continuación, la instancia sigue adquiriendo la memoria que necesita para la carga de trabajo. A medida que se conectan más usuarios y se ejecutan consultas, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquiere la memoria física adicional según la demanda. Una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sigue adquiriendo memoria física hasta que alcanza su asignación de max server memory o hasta que Windows indica que ya no existe más memoria libre; libera memoria cuando se supera el valor de min server memory y Windows indica que hay escasez de memoria libre.

Cuando se inician otras aplicaciones en un equipo que ejecuta una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consumen memoria y la cantidad de memoria física disponible cae por debajo del destino de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ajusta su consumo de memoria. Si se detiene otra aplicación y aumenta la cantidad de memoria disponible, la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aumenta el tamaño de su asignación de memoria. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede liberar y adquirir varios megabytes de memoria cada segundo, lo que le permite ajustarse rápidamente a los cambios de asignación de memoria.


## <a name="effects-of-min-and-max-server-memory"></a>Efectos de las opciones min y max server memory

Las opciones de configuración Memoria de servidor mínima y Memoria de servidor máxima establecen los límites superior e inferior de la cantidad de memoria que utiliza el grupo de búferes del motor de base de datos de Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . El grupo de búferes no adquiere inmediatamente la cantidad de memoria especificada en Memoria de servidor mínima. El grupo de búferes comienza con la memoria precisa para el inicio. Según aumenta la carga de trabajo del motor de base de datos, se sigue adquiriendo la memoria necesaria para permitir la carga de trabajo. El grupo de búferes no libera nada de la memoria adquirida hasta que alcanza la cantidad especificada en Memoria de servidor mínima. Una vez alcanzado el valor de Memoria de servidor mínima, el grupo de búferes utiliza el algoritmo estándar para adquirir y liberar memoria según sea preciso. La única diferencia es que el grupo de búferes nunca deja que su asignación de memoria baje del nivel especificado en Memoria de servidor mínima y adquiera más memoria del nivel especificado en Memoria de servidor máxima.

> [!NOTE]
> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] adquiere, como un proceso, más memoria de la especificada en la opción max server memory. Los componentes tanto internos como externos pueden asignar memoria fuera del grupo de búferes, lo cual consume memoria adicional, pero la memoria asignada en el grupo de búferes normalmente representa la cantidad más grande de memoria que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]consume.


La cantidad de memoria que adquiere el motor de base de datos es totalmente dependiente de la carga de trabajo colocada en la instancia. Una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que no procesa muchas solicitudes nunca podrá alcanzar el nivel de min server memory.

Si se especifica el mismo valor para Memoria de servidor mínima y Memoria de servidor máxima, una vez que la memoria asignada al motor de base de datos alcanza ese valor, el motor de base de datos detiene dinámicamente la adquisición y liberación de la memoria para el grupo de búferes.

Si una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se está ejecutando en un equipo donde se inician o detienen otras aplicaciones con frecuencia, la asignación y cancelación de asignación de memoria por parte de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede ralentizar el inicio de otras aplicaciones. Además, si [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es una de las diversas aplicaciones de servidor que se ejecutan en un único equipo, los administradores del sistema pueden necesitar controlar la cantidad de memoria asignada a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. En estos casos, puede utilizar las opciones Memoria de servidor mínima y Memoria de servidor máxima para controlar cuánta memoria puede usar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obtener más información, vea [Opciones de configuración de memoria del servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md).

Las opciones Memoria de servidor mínima y Memoria de servidor máxima se expresan en megabytes.

## <a name="memory-used-by-includessnoversionincludesssnoversion-mdmd-objects-specifications"></a>Memoria que utilizan las especificaciones de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

La siguiente lista muestra la cantidad de memoria aproximada que usan diferentes objetos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las cantidades mostradas son estimaciones y pueden variar según el entorno y cómo se crean los objetos.

* Bloquear: 64 bytes + 32 bytes por propietario   
* Conexión de usuario: aproximadamente (3* *tamañoDePaqueteDeRed + 94 kb)    

El tamaño del paquete de red es el tamaño de los paquetes del esquema de datos tabulares (TDS) que se utilizan para la comunicación entre las aplicaciones y el motor de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . El tamaño del paquete predeterminado es 4 KB y se controla mediante la opción de configuración Tamaño de paquete de red.

Cuando los conjuntos de resultados activos múltiples (MARS) están habilitados, la conexión de usuario es de aproximadamente (3 + 3 * númeroDeConexionesLógicas) * tamañoDePaqueteDeRed + 94 KB

## <a name="buffer-management"></a>Administración de búfer

El propósito principal de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es almacenar y recuperar datos, por lo que una E/S de disco intensiva es una de las características principales del Motor de base de datos. Debido a que las operaciones de E/S de disco pueden consumir muchos recursos y tardar bastante tiempo en completarse, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se centra en hacer la E/S muy eficaz. La administración de búfer es un componente clave para lograr esta eficacia. El componente de administración de búfer consta de dos mecanismos: el administrador de búfer para obtener acceso a las páginas de bases de datos y actualizarlas y la memoria caché del búfer (también conocida como grupo de búferes) para reducir la E/S de archivos de base de datos. 

### <a name="how-buffer-management-works"></a>Cómo funciona la administración de búfer

Un búfer es un página de 8 KB en memoria (el mismo tamaño que una página de índice o de datos). Por tanto, la memoria caché del búfer está dividida en páginas de 8 kB. El administrador de búfer administra las funciones para la lectura de páginas de índice o de datos de los archivos de disco de base de datos en la caché del búfer y para la escritura de páginas modificadas nuevamente en el disco. Una página permanece en la memoria caché del búfer hasta que el administrador de búfer necesita el área del búfer para leer en ella más datos. Los datos solo vuelven a escribirse en el disco si se han modificado. Los datos de la memoria caché del búfer se pueden modificar varias veces antes de que se vuelvan a escribir en el disco. Para más información, consulte [Leer páginas](../relational-databases/reading-pages.md) y [Escribir páginas](../relational-databases/writing-pages.md).

Cuando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se inicia, calcula el tamaño del espacio de direcciones virtuales de la caché de búferes basándose en un número de parámetros, como la cantidad de memoria física en el sistema, el número configurado de subprocesos máximos de servidor y varios parámetros de inicio. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reserva la cantidad calculada de su espacio de direcciones virtuales del proceso (llamado destino de memoria) para la caché de búferes, pero solo adquiere (confirma) la cantidad necesaria de memoria física para la carga actual. Puede realizar una consulta en las columnas **bpool_commit_target** y **bpool_committed** en la vista de catálogo [sys.dm_os_sys_info](../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md) para devolver el número de páginas reservadas como memoria objetivo y el número de páginas actualmente confirmadas en la caché del búfer, respectivamente.

El intervalo entre el inicio de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y el momento en que la caché del búfer obtiene su memoria objetivo se llama arranque. Durante este período, las solicitudes de lectura llenan los búferes según sea necesario. Por ejemplo, una solicitud de lectura de una página llena una única página de búfer. Esto significa que el arranque depende del número y el tipo de solicitudes del cliente. El arranque se agiliza mediante la transformación de solicitudes de lectura de una página en solicitudes de ocho páginas alineadas. Esto permite que el arranque finalice mucho más rápido, especialmente en equipos con mucha memoria.

Debido a que el administrador de búfer utiliza la mayor parte de la memoria en el proceso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , coopera con el administrador de memoria para permitir que otros componentes utilicen sus búferes. El administrador de búfer interactúa principalmente con los siguientes componentes:

* Administrador de recursos, para controlar la utilización de memoria general y, en plataformas de 32 bits, para controlar el uso del espacio de direcciones.  
* Administrador de bases de datos y [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Operating System (SQLOS), para operaciones de E/S de archivos de bajo nivel.  
* Administrador de registros, para registros de escritura anticipada.  

### <a name="supported-features"></a>Características admitidas

El administrador de búfer admite las características siguientes:

* El administrador de búfer está preparado para el acceso no uniforme a memoria (NUMA, Non-Uniform Memory Access). Las páginas de la caché del búfer se distribuyen por los nodos NUMA de hardware, que permiten que un subproceso tenga acceso a una página de búfer que esté asignada en el nodo NUMA local y no desde una memoria externa. 
* El administrador de búfer admite la función de Agregar memoria sin interrupción, que permite a los usuarios agregar memoria física sin reiniciar el servidor. 
* El administrador de búfer admite páginas grandes en plataformas de 64 bits. El tamaño de página es específico de la versión de Windows. 
* El administrador de búfer proporciona diagnósticos adicionales que se muestran mediante vistas de administración dinámica. Puede utilizar estas vistas para supervisar diversos recursos del sistema operativo específicos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por ejemplo, puede usar la vista sys.dm_os_buffer_descriptors para supervisar las páginas de la caché del búfer.   

### <a name="disk-io"></a>E/S de disco
El administrador de búfer solo realiza tareas de lectura y escritura en la base de datos. Las otras operaciones con archivos, como la apertura, el cierre, la extensión y la reducción, las realizan el administrador de base de datos y los componentes del administrador de archivos. 

Las operaciones de E/S de disco que realiza el administrador de búfer tienen las siguientes características:

* Todas las operaciones de E/S se realizan de forma asincrónica, lo que permite que el subproceso de llamada siga con el procesamiento mientras la operación de E/S se realiza en segundo plano.
* Todas las operaciones de E/S se emiten en los subprocesos de llamada a menos que la opción affinity I/O (E/S de afinidad) esté en uso. La opción de máscara de afinidad de E/S enlaza la E/S del disco de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un subconjunto específico de unidades CPU. En entornos de procesamiento de transacciones en línea (OLTP) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de grandes prestaciones, esta extensión puede mejorar el rendimiento de los subprocesos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que emiten E/S.
* Las operaciones de E/S de múltiples páginas se logran con E/S por dispersión y recopilación, que permite transferir datos a áreas no contiguas de memoria, o desde ellas. Esto significa que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede llenar o vaciar rápidamente la caché del búfer y, a la vez, evitar múltiples solicitudes de E/S física. 

#### <a name="long-io-requests"></a>Solicitudes de E/S larga  
El administrador de búfer informa sobre cualquier solicitud de E/S que haya quedado pendiente durante al menos 15 segundos. Esto ayuda al administrador del sistema a distinguir entre problemas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y problemas del subsistema de E/S. El mensaje de error 833 se notifica y aparece en el registro de errores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de la siguiente forma:

`` 
SQL Server has encountered %d occurrence(s) of I/O requests taking longer than %d seconds to complete on file [%ls] in database [%ls] (%d). The OS file handle is 0x%p. The offset of the latest long I/O is: %#016I64x.
`` 

Una E/S larga puede ser de lectura o de escritura, pero esto no se indica actualmente en el mensaje. Los mensajes de E/S larga son advertencias, no errores. No indican problemas con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Los mensajes se notifican para ayudar a los administradores del sistema a encontrar la causa de los tiempos de respuesta largos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con mayor rapidez y a distinguir problemas que estén fuera del control de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por eso, no es necesario tomar ninguna acción, pero el administrador del sistema debe investigar por qué la solicitud de E/S tardó tanto tiempo y si ese tiempo es justificable.

#### <a name="causes-of-long-io-requests"></a>Causas de solicitudes de E/S largas  
Un mensaje de E/S larga puede indicar que una E/S está permanente bloqueada y que nunca se completará (lo que también se conoce como E/S perdida) o que simplemente no se completó aún. No es posible saber con los datos del mensaje de qué caso se trata, aunque una E/S perdida casi siempre llevará a un tiempo de espera de bloqueo temporal.

Las E/S largas suelen indicar una carga de trabajo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] demasiado intensa para el subsistema de disco. Se puede indicar un subsistema de disco inadecuado cuando:

* Aparecen múltiples mensajes de E/S largas en el registro de errores durante una carga de trabajo pesada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .
* Los contadores de rendimiento muestran latencias de disco prolongadas, colas de disco largas o no muestran el tiempo de inactividad de disco.  

Otra posible causa de las E/S largas es que un componente de la ruta de acceso de E/S (por ejemplo, un controlador o el firmware) posponga de forma continua el servicio para una solicitud de E/S antigua en favor de dar servicio a solicitudes nuevas que están más cerca de la posición actual del cabezal del disco. La técnica corriente de procesar solicitudes según su prioridad sobre la base de las que están más cerca de la posición actual del cabezal de lectura/escritura se conoce como "búsqueda de elevador". Esto puede resultar difícil de corroborar con la herramienta Monitor del sistema de Windows (PERFMON.EXE) porque a la mayor parte de las E/S se las da servicio inmediatamente. Las solicitudes de E/S largas pueden agravarse con cargas de trabajo que realicen un gran número de operaciones de E/S secuenciales, como copias de seguridad y restauración, recorridos de tabla, ordenaciones, creación de índices, cargas masivas y puestas a cero de archivos.

Las E/S largas aisladas que no están relacionadas con ninguna de las situaciones anteriores pueden estar causadas por un problema con el hardware o el controlador. El registro de eventos del sistema puede contener un evento relacionado que ayude a diagnosticar el problema.

#### <a name="error-detection"></a>Detección de errores  
Las páginas de bases de datos pueden utilizar uno de los dos mecanismos opcionales que ayudan a garantizar la integridad de la página desde el momento en que se escribe en el disco hasta que se vuelve a leer: protección contra página rasgada y protección de suma de comprobación. Estos mecanismos permiten emplear un método independiente para comprobar la corrección, no solo del almacenamiento de datos, sino también de los componentes de hardware, como controladores, cables e incluso el sistema operativo. La protección se agrega a la página justo antes de escribirla en el disco y se comprueba después de que se lee desde el disco.

#### <a name="torn-page-protection"></a>Protección contra página rasgada  
La protección contra página rasgada, que se introdujo en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000, es básicamente una forma de detectar errores en las páginas a causa de problemas con el suministro eléctrico. Por ejemplo, es posible que por un problema con el suministro eléctrico solo se escriba una parte de la página en el disco. Cuando se utiliza la protección contra página rasgada, se coloca una firma de 2 bits al final de cada segmento de 512 bytes en la página (después de haber copiado los dos bits originales en el encabezado de la página). La firma alterna entre los binarios 01 y 10 en cada escritura, por lo que siempre es posible detectar las ocasiones en que solo una parte de los sectores las hicieron en el disco: si hay un bit con el estado incorrecto cuando la página se lee posteriormente, la página se escribió de forma incorrecta y se detecta una página rasgada. La detección de página rasgada utiliza un mínimo de recursos; sin embargo, no detecta todos los errores causados por errores del hardware de disco.

#### <a name="checksum-protection"></a>Protección de suma de comprobación  
La protección de suma de comprobación, característica implementada en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005, proporciona una comprobación de integridad de datos más sólida. Se calcula una suma de comprobación para los datos de cada página que se escribe y se almacena en el encabezado de la página. Cada vez que se lee desde disco una página con una suma de comprobación almacenada, el motor de base de datos vuelve a calcular la suma de comprobación para los datos de la página y muestra el error 824 cuando la nueva suma de comprobación no coincide con la suma almacenada. La protección de suma de comprobación puede detectar más errores que la protección contra página rasgada porque tiene en cuenta cada byte de la página; sin embargo, consume una cantidad de recursos considerable. Cuando la suma de comprobación está habilitada, pueden detectarse los errores debidos a cualquier problema con el suministro eléctrico o a hardware o firmware defectuosos cada vez que el administrador de búfer lea una página del disco.

El tipo de protección de página que se utilice es un atributo de la base de datos que contiene la página. La protección de suma de comprobación es la protección predeterminada para bases de datos creadas en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2005 y en versiones posteriores. El mecanismo de protección de páginas se especifica al crear la base de datos y se puede modificar con ALTER DATABASE. La configuración de protección de página actual se puede determinar consultando la columna page_verify_option de la vista de catálogo [sys.databases](../relational-databases/system-catalog-views/sys-databases-transact-sql.md) o la propiedad IsTornPageDetectionEnabled de la función [DATABASEPROPERTYEX](../t-sql/functions/databasepropertyex-transact-sql.md) . Si se modifica la configuración de protección de página, la nueva configuración no afecta a toda la base de datos de forma inmediata. En cambio, las páginas adoptan el nivel de protección actual de la base de datos cuando se vuelven a escribir. Esto significa que la base de datos puede estar compuesta de páginas con distintos tipos de protección. 

## <a name="understanding-non-uniform-memory-access"></a>Descripción del acceso no uniforme a memoria

Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está preparado para el acceso no uniforme a memoria (NUMA) y realiza un buen rendimiento en hardware NUMA sin necesidad de establecer ninguna configuración especial. A medida que aumentan la velocidad del reloj y el número de procesadores, resulta cada vez más difícil reducir la latencia de la memoria necesaria para utilizar esta potencia de procesamiento adicional. Para evitarlo, los proveedores de hardware proporcionan cachés L3 grandes, pero esto es solo una solución limitada. La arquitectura NUMA proporciona una solución escalable para este problema. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ha diseñado para aprovechar los equipos basados en NUMA sin necesidad de realizar cambios en las aplicaciones. Para obtener más información, vea [Cómo configurar SQL Server para que use NUMA de software](../database-engine/configure-windows/soft-numa-sql-server.md).

## <a name="see-also"></a>Vea también
[Leer páginas](../relational-databases/reading-pages.md)   
 [Escribir páginas](../relational-databases/writing-pages.md)


