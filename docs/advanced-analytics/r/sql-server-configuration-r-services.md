---
title: "Configuración de SQL Server (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: dbd29457adf7a3dd05211c2dc0688d45a54e405e
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuración de SQL Server para su uso con R

En este artículo es el segundo de una serie que describe la optimización de rendimiento para servicios de R que se basa en dos casos prácticos.  En este artículo se proporciona instrucciones sobre la configuración de hardware y de red del equipo que se usa para ejecutar SQL Server R Services. También contiene información acerca de las maneras de configurar la instancia de SQL Server, base de datos o tablas que se utilizan en una solución. Dado que el uso de NUMA en SQL Server difumina las líneas entre las optimizaciones de hardware y base de datos, una tercera sección describe CPU afinamiento y regulación de recursos en detalle.

> [!TIP]
> Si está familiarizado con SQL Server, recomendamos encarecidamente que revise también la Guía de optimización de rendimiento de SQL Server: [Monitor y debería ajustar para obtener un rendimiento](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Optimización de hardware

Optimización del equipo del servidor es importante para asegurarse de que tiene los recursos necesarios para ejecutar scripts externos. Cuando los recursos son limitados, puede aparecer síntomas como los siguientes:

- Ejecución del trabajo es diferida o cancela, para dar prioridad a otras operaciones de base de datos
- Script de R que producen error "superado la cuota" para finalizar sin finalizar
- Datos cargados en memoria de R truncado para resultados incompletos

### <a name="memory"></a>Memoria

La cantidad de memoria disponible en el equipo puede afectar considerablemente al rendimiento de los algoritmos de análisis avanzado. Memoria insuficiente puede afectar el grado de paralelismo cuando se usa el contexto de proceso SQL. También puede afectar al tamaño de los fragmentos (filas por operación de lectura) que se puede procesar y al número de sesiones simultáneas que se admiten.

Se recomienda un mínimo de 32 GB. Si tiene más de 32 GB disponible, puede configurar el origen de datos SQL para utilizar más filas en cada operación de lectura para mejorar el rendimiento.

También puede administrar la memoria utilizada por la instancia. De forma predeterminada, SQL Server se establece una prioridad a los procesos de script externo cuando se asignó la memoria. En una instalación predeterminada de servicios de R, solo el 20% de memoria disponible se asigna a R.

Normalmente esto no es suficiente para tareas de ciencia de datos, pero tampoco es conveniente que se agote el servidor SQL server de memoria. Debe probar y ajustar la asignación de memoria entre el motor de base de datos, servicios relacionados y los scripts externos, con la suposición de que la configuración óptima varía caso por caso.

Para el modelo de coincidencia de reanudación, el uso de script externo fue elevado y no hay ninguna otra base de datos servicios del motor de ejecución; por lo tanto, los recursos asignados a los scripts externos se aumentaran al 70%, que era la mejor configuración para el rendimiento de la secuencia de comandos.

### <a name="power-options"></a>Opciones energía

En el sistema operativo Windows, la **de alto rendimiento** debe utilizarse la opción de energía. Mediante la configuración de energía diferente da como resultado un rendimiento reducido o incoherente cuando usa SQL Server.

### <a name="disk-io"></a>E/S de disco

Aprendizaje y la predicción trabajos mediante R Services son de forma inherente E/S enlazadas y dependen de la velocidad de los discos que se almacena la base de datos en. Unidades de disco más rápidas, como unidades de estado sólido (SSD) pueden ayudar.

La E/S de disco también se ve afectada por otras aplicaciones que obtienen acceso al disco, por ejemplo, las operaciones de lectura en una base de datos mediante otros clientes. El rendimiento de E/S de disco también se puede ver afectado por la configuración del sistema de archivos que se use, como el tamaño de bloque usado por el sistema de archivos.

Si hay varias unidades, almacén de las bases de datos en una unidad distinta de SQL Server, por lo que solicita para el motor de base de datos no están alcanzando el mismo disco que las solicitudes para los datos almacenados en la base de datos.

La E/S de disco también puede afectar considerablemente al rendimiento cuando se ejecutan funciones analíticas RevoScaleR que usan varias iteraciones durante el entrenamiento. Por ejemplo, `rxLogit`, `rxDTree`, `rxDForest`, y `rxBTrees` todos utilizan varias iteraciones. Cuando el origen de datos es SQL Server, estos algoritmos utilizan archivos temporales que se optimizan para capturar los datos. Estos archivos se limpian automáticamente una vez finalizada la sesión. Tener un disco de alto rendimiento para las operaciones de lectura/escritura puede mejorar significativamente el tiempo global transcurrido para estos algoritmos.

> [!NOTE]
> Las versiones anteriores de R Services requieren la compatibilidad con nombre de archivo 8.3 en sistemas operativos Windows. Esta restricción se soluciona después de Service Pack 1. Sin embargo, puede usar fsutil.exe para determinar si una unidad es compatible con los nombres de 8.3 archivo, o para habilitar la compatibilidad si no es así.

### <a name="paging-file"></a>Archivo de paginación

El sistema operativo Windows usa un archivo de paginación para administrar los volcados de memoria y para almacenar páginas de memoria virtual. Si observa una paginación excesiva, considere la posibilidad de aumentar la memoria física del equipo. Aunque el hecho de tener más memoria física no elimina la paginación, reduce la necesidad de paginación.

La velocidad del disco en el que se almacena el archivo de paginación también puede afectar al rendimiento. Si se almacena el archivo de paginación en un SSD o si se usan varios archivos de paginación en varios SSD, puede mejorar el rendimiento.

Para obtener información sobre el archivo de paginación de ajuste de tamaño, vea [cómo determinar el tamaño del archivo de página adecuado para las versiones de 64 bits de Windows](https://support.microsoft.com/en-us/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Optimizaciones en el nivel de instancia o base de datos

Optimización de la instancia de SQL Server es la clave para una ejecución eficaz de scripts externos.

> [!NOTE]
> Los valores óptimos varían según el tamaño y el tipo de los datos, el número de columnas que se usa para la puntuación o entrenar un modelo.
> 
> Puede revisar los resultados de las optimizaciones específicas en el artículo final: [Performance Tuning - resultados del estudio de caso](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Para las secuencias de comandos de ejemplo, vea el separar [repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Compresión de tabla

A menudo se puede mejorar el rendimiento de E/S mediante el uso de compresión o un almacén de datos en columnas. Por lo general, los datos a menudo se repiten en varias columnas dentro de una tabla, para usar un almacén de columnas aprovecha las ventajas de estas repeticiones al comprimir los datos.

Un almacén de columnas no sea tan eficaz si hay muchas inserciones en la tabla, pero es una buena opción si los datos son estáticos o solo cambian con poca frecuencia. Si un almacén de columnas no es adecuado, se puede usar la compresión en una tabla principal de fila para mejorar la E/S.

Para obtener más información, vea los documentos siguientes:

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar la compresión en una tabla o índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guía de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tablas con optimización para memoria

Hoy en día, la memoria ya no es un problema para los equipos modernos. Tal y como especificaciones de hardware continuarán mejorando, es relativamente fácil de obtener memoria RAM en valores correctos. Sin embargo, al mismo tiempo, se está produciendo datos más rápidamente que nunca, y se deben procesar los datos con una latencia baja.

Tablas optimizadas en memoria representan una solución en que aprovechan la gran cantidad de memoria disponible en los equipos avanzados para abordar el problema de grandes cantidades de datos. Tablas optimizadas en memoria principalmente residen en la memoria, para que sea de lectura de datos y se escriben en la memoria. Para que la durabilidad, una segunda copia de la tabla se mantiene en el disco y datos solo se leen desde el disco durante la recuperación de la base de datos.

Si tiene que leer y escribir en las tablas con frecuencia, las tablas optimizadas en memoria pueden ayudarle a alta escalabilidad y una baja latencia.  En el escenario de coincidencia de reanudación, permite el uso de tablas optimizadas en memoria que leer todas las características de reanudación de la base de datos y almacenarlos en la memoria principal, para que coincidan con las ofertas de trabajo nuevo. Esto reduce considerablemente el E/S de disco.

Se obtienen mejoras de rendimiento adicionales mediante el uso de la tabla optimizada en memoria en el proceso de escritura diferida de predicciones a la base de datos de varios procesos por lotes simultáneos. El uso de tablas optimizadas en memoria en SQL Server habilitado baja latencia en la tabla lecturas y escrituras.

La experiencia también estaba sin problemas durante el desarrollo. Tablas optimizadas para memoria perdurables se crearon al mismo tiempo que se creó la base de datos. Por lo tanto, desarrollo usa el mismo flujo de trabajo, independientemente de dónde se almacenan los datos.

### <a name="processor"></a>Procesador

SQL Server puede realizar tareas en paralelo mediante núcleos disponibles en el equipo; el más núcleos que están disponibles, mejor será el rendimiento. Aunque no puede ser útil aumentar el número de núcleos para operaciones de E/S enlazado, CPU había enlazada beneficio de algoritmos de CPU más rápidas con varios núcleos.

Dado que el servidor se usa normalmente por varios usuarios al mismo tiempo, el Administrador de base de datos debe determinar el número ideal de núcleos que se necesitan para admitir cálculos de máxima carga de trabajo.

### <a name="resource-governance"></a>Regulador de recursos

En las ediciones que admiten el regulador de recursos, puede utilizar grupos de recursos para especificar que ciertas cargas de trabajo se asignan a un número de CPU. También puede administrar la cantidad de memoria asignada a cargas de trabajo específicas.

La regulación de recursos de SQL Server le permite centralizar la supervisión y control de los distintos recursos que usan SQL Server y R. Por ejemplo, podría asignar la mitad de la memoria disponible para el motor de base de datos, para asegurarse de que core services siempre se puedan ejecutar a pesar de las cargas de trabajo más pesadas transitorios.

El valor predeterminado para el consumo de memoria por scripts externos se limita a 20% de la memoria total disponible para SQL Server. Este límite se aplica de forma predeterminada para asegurarse de que todas las tareas que se basan en el servidor de base de datos no se ven gravemente afectadas por los trabajos de larga ejecución R. Pero el administrador de bases de datos puede cambiar estos límites. En muchos casos, el límite de 20% no es suficiente para admitir las cargas de trabajo de aprendizaje de automático grave.

Las opciones de configuración admitidas son **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, y **MAX_PROCESSES**. Para ver la configuración actual, use esta instrucción:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  Si el servidor se utiliza principalmente para R Services, puede resultar útil aumentar MAX_CPU_PERCENT hasta un 40% o 60%.

-  Si la cantidad de sesiones de R debe usar el mismo servidor al mismo tiempo, se deben aumentar las tres opciones.

Para cambiar los valores de los recursos asignados, use las instrucciones de T-SQL.

+ Esta instrucción establece el uso de memoria al 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Esta instrucción establece los tres valores configurables:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Si cambia una memoria, la CPU o la configuración del proceso máximo y, a continuación, deberá aplicar la configuración inmediatamente, ejecute esta instrucción:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Afinidad de CPU, de NUMA de hardware y NUMA de software

Cuando se usa SQL Server como el contexto de proceso, a veces puede conseguir un mejor rendimiento ajustando la configuración relacionada con la afinidad del procesador y de NUMA. 

Sistemas con _NUMA de hardware_ tiene más de un bus del sistema, cada una sirve para un pequeño conjunto de procesadores. Cada CPU puede tener acceso a la memoria asociada a otros grupos de forma coherente. Cada grupo se denomina nodo NUMA. Si tiene NUMA de hardware, lo puede configurar para que utilice memoria intercalada en vez de NUMA. En ese caso, Windows y, por tanto, SQL Server lo no reconocerán como NUMA. 

Puede ejecutar la consulta siguiente para buscar el número de nodos de memoria disponibles para SQL Server:

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Si la consulta devuelve un único nodo de memoria (nodo 0), no tiene NUMA de hardware o el hardware está configurado como intercalado (no NUMA). SQL Server también omite NUMA de hardware cuando hay cuatro o menos CPU, o si al menos un nodo tiene únicamente una CPU.

Si el equipo tiene varios procesadores, pero no tiene NUMA de hardware, también puede usar [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) para subdividir CPU en grupos más pequeños.  En SQL Server 2016 y 2017 de SQL Server, la característica Soft-NUMA se habilita automáticamente al iniciar el servicio de SQL Server.

Cuando se habilita Soft-NUMA, SQL Server administra automáticamente los nodos en su nombre; Sin embargo, para optimizar cargas de trabajo específicas, puede deshabilitar _la afinidad parcial_ y configurar manualmente la afinidad de CPU para los nodos NUMA de software. Esto puede proporcionarle más control sobre el que se asignan las cargas de trabajo a otros nodos, especialmente si está usando una edición de SQL Server que admite regulador de recursos. Al especificar la afinidad de CPU y Alinear grupos de recursos con grupos de CPU, puede reducir la latencia y garantizar que los procesos relacionados se realizan en el mismo nodo NUMA.

El proceso general de configuración de NUMA de software y la afinidad de CPU para admitir las cargas de trabajo de R es el siguiente:

1. Habilitar soft-NUMA, si está disponible
2. Definir la afinidad del procesador
3. Crear grupos de recursos para los procesos externos, mediante [regulador de recursos](../r/resource-governance-for-r-services.md)
4. Asigne el [grupos de cargas de trabajo](../../relational-databases/resource-governor/resource-governor-workload-group.md) a determinados grupos de afinidad

Para obtener más información, incluido el código de ejemplo, vea este tutorial: [SQL optimización sugerencias y trucos (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Otros recursos:**

+ [Soft-NUMA en SQL Server](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Cómo asignar nodos NUMA de software a las CPU

+ [Soft-NUMA automático: solo se ejecuta más rápido (Bob Ward)](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   Describe el historial, así como detalles de implementación, con el rendimiento en los servidores de varios núcleos más recientes.

## <a name="task-specific-optimizations"></a>Optimizaciones específicas de tareas

En esta sección se resume los métodos adoptados en estos casos prácticos y en otras pruebas para optimizar las cargas de trabajo de aprendizaje específicos del equipo. Cargas de trabajo comunes incluyen entrenamiento del modelo, extracción de características e ingeniería de característica y distintos escenarios de puntuación: varias filas, lote pequeño y lote de gran tamaño.

### <a name="feature-engineering"></a>Ingeniería de características

Una dificultad con R es que normalmente se procesan en una sola CPU. Se trata de un cuello de botella de rendimiento principales para realizar muchas tareas, especialmente la ingeniería de características. En la solución de coincidencia de reanudación, la tarea de ingeniería de características solo crea 2.500 características de producto cruzado que tuvieron que combinarse con las características de 100 originales. Esta tarea tardaría una cantidad considerable de tiempo si todo se realiza en una sola CPU.

Hay varias maneras de mejorar el rendimiento de ingeniería de características. Puede optimizar el código de R y mantener la extracción de características dentro del proceso de modelado o mover el proceso de ingeniería de características a SQL.

- Uso de R. Definir una función y, a continuación, se pasa como el argumento a [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante el entrenamiento. Si el modelo admite el procesamiento en paralelo, se puede procesar el trabajo de ingeniería de característica con varias CPU. Con este enfoque, el equipo de ciencia de datos observados una mejora del rendimiento de 16% en términos de tiempo de puntuación. Sin embargo, este enfoque requiere un modelo que admite la ejecución en paralelo y una consulta que se puede ejecutar con un plan paralelo.

- Contexto de proceso de R de uso con una instancia de SQL. En un entorno con varios procesadores con aislado recursos disponibles para la ejecución de lotes independientes, puede lograr una mayor eficacia al aislar las consultas SQL usadas para cada lote, para extraer datos de tablas y restringir los datos en el mismo grupo de cargas de trabajo. Los métodos usados para aislar los lotes incluyen la creación de particiones y uso de PowerShell para ejecutar consultas independientes en paralelo.

- La ejecución en paralelo ad hoc: contexto de proceso en un SQL Server, puede basarse en el motor de base de datos SQL para exigir la ejecución en paralelo si es posible y si no se encuentra esa opción para ser más eficaz.

- Usar T-SQL en un proceso independiente de características. Cálculo previo de los datos de característica con SQL suele ser más rápido.

### <a name="prediction-scoring-in-parallel"></a>Predicción (puntuación) en paralelo

Una de las ventajas de SQL Server es su capacidad para manejar un gran volumen de filas en paralelo. En ningún sitio por lo que se marca esta ventaja como en la puntuación. Por lo general el modelo no necesita acceso a todos los datos para puntuación, por lo que puede dividir los datos de entrada, con cada grupo de cargas de trabajo, una tarea de procesamiento.

También puede enviar los datos de entrada como una sola consulta, y SQL Server, a continuación, analiza la consulta. Si un plan de consulta paralelo se puede crear para los datos de entrada, automáticamente crea particiones de datos asignados a los nodos y realiza requiere combinaciones y agregaciones en paralelo también.

Si está interesado en los detalles de cómo definir un procedimiento almacenado para su uso para determinar la puntuación, vea el proyecto de ejemplo en [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) y busque el archivo "step5_score_for_matching.sql". El ejemplo de secuencia de comandos también inicio de la consulta realiza un seguimiento y horas de finalización y escribe la hora en la consola SQL para que se pueda evaluar el rendimiento.

### <a name="concurrent-scoring-using-resource-groups"></a>Puntuación simultáneas con grupos de recursos

Para escalar el problema de puntuación, una práctica recomendada consiste en adoptar el enfoque de asignar/reducir en el que millones de elementos se dividen en varios lotes. A continuación, varios trabajos de puntuación se ejecutan simultáneamente. En este marco de trabajo son los lotes procesados en diferentes conjuntos de CPU, y los resultados se recopilan y se vuelve a escribir en la base de datos.

Este es el enfoque usado en el escenario de coincidencia de reanudación; Sin embargo, el regulador de recursos de SQL Server es esencial para implementar este enfoque. Mediante la configuración de grupos de cargas de trabajo para los trabajos de script externo, puede enrutar R puntuación trabajos a los grupos de procesador distinta y lograr un rendimiento más rápido.

La regulación de recursos también puede ayudar a asignar repartir los recursos disponibles en el servidor (CPU y memoria) para minimizar la competencia de cargas de trabajo. Puede configurar las funciones clasificadoras para distinguir entre diferentes tipos de trabajos de R: por ejemplo, podría decidir que la puntuación llama desde una aplicación siempre tiene prioridad, mientras reconversión trabajos tienen una prioridad baja. Este aislamiento de recursos podría mejorar el tiempo de ejecución y proporcionar un rendimiento más predecible.

### <a name="concurrent-scoring-using-powershell"></a>Puntuación simultáneas con PowerShell

Si decide dividir los datos usted mismo, puede utilizar scripts de PowerShell para ejecutar varias tareas simultáneas de puntuación. Para ello, use el cmdlet Invoke-SqlCmd e iniciar las tareas de puntuación en paralelo.

En el escenario de coincidencia de reanudación, simultaneidad se diseñó como sigue:

- 20 procesadores se dividen en cuatro grupos de cinco CPUs. Cada grupo de CPU está ubicado en el mismo nodo NUMA.

- Número máximo de procesos por lotes simultáneos se estableció en ocho.

- Cada grupo de cargas de trabajo debe controlar dos tareas de puntuación. Tan pronto como una tarea ha finalizado la lectura de datos e inicia la puntuación, la otra tarea puede comenzar a leer los datos de la base de datos.

Para ver las secuencias de comandos de PowerShell para este escenario, abra el experiment.ps1 de archivo en el [Github proyecto](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Almacenar modelos de predicción

Cuando el aprendizaje y evaluación finaliza y se ha seleccionado un mejor modelo, es recomendable que almacene el modelo en la base de datos para que esté disponible para las predicciones. Cargar el modelo previamente calculado de la base de datos para la predicción es eficaz, ya que aprendizaje automático de SQL Server usa algoritmos de serialización especial para almacenar y cargar modelos al mover entre R y la base de datos.

> [!TIP]
> En SQL Server 2017, puede utilizar la función de PREDICCIÓN para realizar puntuaciones incluso si R no está instalado en el servidor. Se admiten tipos de modelos limitado, desde el paquete RevoScaleR.

Sin embargo, dependiendo del algoritmo que utilice, algunos modelos pueden ser bastante grandes, sobre todo cuando entrenado en un gran conjunto de datos. Por ejemplo, los algoritmos como **lm** o **glm** generar una gran cantidad de resumen datos junto con las reglas. Dado que no hay límite en el tamaño de un modelo que se pueden almacenar en una columna varbinary, se recomienda eliminar los artefactos innecesarios del modelo antes de almacenar el modelo en la base de datos de producción.

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Rendimiento para la optimización de R: Introducción](../r/sql-server-r-services-performance-tuning.md)

[Ajuste del rendimiento de R - configuración de SQL Server](../r/sql-server-configuration-r-services.md)

[Ajuste del rendimiento de R - R optimización del código y los datos](../r/r-and-data-optimization-r-services.md)

[Ajuste del rendimiento: resultados del estudio de caso](../r/performance-case-study-r-services.md)

