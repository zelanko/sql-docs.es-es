---
title: Configuración de SQL Server (R Services)
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: feb59ac529b0a66603d9e8b901e9755588ac0379
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344850"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuración de SQL Server para su uso con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo es el segundo de una serie que describe la optimización del rendimiento de R Services en función de dos casos prácticos.  En este artículo se proporcionan instrucciones sobre el hardware y la configuración de red del equipo que se utiliza para ejecutar SQL Server R Services. También contiene información sobre las formas de configurar la instancia de SQL Server, la base de datos o las tablas que se usan en una solución. Dado que el uso de NUMA en SQL Server desenfoca la línea entre las optimizaciones de hardware y de base de datos, en una tercera sección se describe detalladamente la affinitization de la CPU y el gobierno de recursos.

> [!TIP]
> Si no está familiarizado con SQL Server, le recomendamos encarecidamente que revise también la guía de optimización del rendimiento de SQL Server: [Supervisar y optimizar el rendimiento](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Optimización de hardware

La optimización del equipo servidor es importante para asegurarse de que tiene los recursos necesarios para ejecutar scripts externos. Cuando los recursos están limitados, puede ver síntomas como los siguientes:

- La ejecución del trabajo se aplaza o se cancela para dar prioridad a otras operaciones de base de datos
- Error "cuota superada" que hace que el script de R finalice sin finalización
- Datos cargados en la memoria de R truncados, para resultados incompletos

### <a name="memory"></a>Memoria

La cantidad de memoria disponible en el equipo puede afectar considerablemente al rendimiento de los algoritmos de análisis avanzado. La memoria insuficiente podría afectar al grado de paralelismo cuando se usa el contexto de cálculo de SQL. También puede afectar al tamaño de los fragmentos (filas por operación de lectura) que se puede procesar y al número de sesiones simultáneas que se admiten.

Se recomienda un mínimo de 32 GB. Si tiene más de 32 GB disponibles, puede configurar el origen de datos SQL para que use más filas en cada operación de lectura para mejorar el rendimiento.

También puede administrar la memoria que usa la instancia de. De forma predeterminada, SQL Server se prioriza en los procesos de script externos cuando se asigna la memoria. En una instalación predeterminada de R Services, solo se asigna un 20% de la memoria disponible a R.

Por lo general, esto no es suficiente para las tareas de ciencia de datos, pero ninguna de las cuales desea privar de memoria de SQL Server. Debe experimentar y ajustar la asignación de memoria entre el motor de base de datos, los servicios relacionados y los scripts externos, sabiendo que la configuración óptima varía entre mayúsculas y minúsculas.

Para el modelo de búsqueda de coincidencias, el uso de scripts externos era pesado y no había otros servicios de motor de base de datos en ejecución; por lo tanto, los recursos asignados a los scripts externos se aumentaron al 70%, que era la mejor configuración para el rendimiento del script.

### <a name="power-options"></a>Opciones energía

En el sistema operativo Windows, se debe usar la opción de energía **alto rendimiento** . El uso de una configuración de energía diferente produce un rendimiento reducido o incoherente al utilizar SQL Server.

### <a name="disk-io"></a>E/S de disco

Los trabajos de entrenamiento y predicción que usan R Services están enlazados de manera inherente a la e/s y dependen de la velocidad de los discos en los que está almacenada la base de datos. Las unidades más rápidas, como las unidades de estado sólido (SSD), pueden ayudar.

La E/S de disco también se ve afectada por otras aplicaciones que obtienen acceso al disco, por ejemplo, las operaciones de lectura en una base de datos mediante otros clientes. El rendimiento de E/S de disco también se puede ver afectado por la configuración del sistema de archivos que se use, como el tamaño de bloque usado por el sistema de archivos.

Si hay disponibles varias unidades, almacene las bases de datos en una unidad diferente de SQL Server para que las solicitudes del motor de base de datos no se encuentren en el mismo disco que las solicitudes de datos almacenados en la base de datos.

La E/S de disco también puede afectar considerablemente al rendimiento cuando se ejecutan funciones analíticas RevoScaleR que usan varias iteraciones durante el entrenamiento. Por ejemplo, `rxLogit` `rxDTree` `rxBTrees` ,, y usan varias iteraciones. `rxDForest` Cuando se SQL Server el origen de datos, estos algoritmos usan archivos temporales que están optimizados para capturar los datos. Estos archivos se limpian automáticamente una vez finalizada la sesión. Tener un disco de alto rendimiento para las operaciones de lectura y escritura puede mejorar significativamente el tiempo total transcurrido para estos algoritmos.

> [!NOTE]
> Las primeras versiones de R Services requerían compatibilidad con el nombre de archivo 8,3 en los sistemas operativos Windows. Esta restricción se ha levantado después del Service Pack 1. Sin embargo, puede usar fsutil. exe para determinar si una unidad admite nombres de archivo 8,3 o para habilitar la compatibilidad si no la admite.

### <a name="paging-file"></a>Archivo de paginación

El sistema operativo Windows usa un archivo de paginación para administrar los volcados de memoria y para almacenar páginas de memoria virtual. Si observa una paginación excesiva, considere la posibilidad de aumentar la memoria física del equipo. Aunque el hecho de tener más memoria física no elimina la paginación, reduce la necesidad de paginación.

La velocidad del disco en el que se almacena el archivo de paginación también puede afectar al rendimiento. Si se almacena el archivo de paginación en un SSD o si se usan varios archivos de paginación en varios SSD, puede mejorar el rendimiento.

Para obtener información sobre el ajuste de tamaño del archivo de paginación, consulte [cómo determinar el tamaño de archivo de página adecuado para las versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Optimizaciones en el nivel de instancia o de base de datos

La optimización de la instancia de SQL Server es la clave para la ejecución eficaz de los scripts externos.

> [!NOTE]
> La configuración óptima varía en función del tamaño y el tipo de los datos, el número de columnas que se usan para puntuar o entrenar un modelo.
> 
> Puede revisar los resultados de las optimizaciones específicas en el artículo final: [Optimización del rendimiento: resultados de los casos prácticos](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Para obtener scripts de ejemplo, vea el [repositorio de github](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)independiente.

### <a name="table-compression"></a>Compresión de tabla

A menudo, el rendimiento de e/s se puede mejorar mediante compresión o un almacén de datos en columnas. Normalmente, los datos se repiten con frecuencia en varias columnas de una tabla, por lo que el uso de un almacén de columnas saca provecho de estas repeticiones al comprimir los datos.

Un almacén de columnas puede no ser tan eficaz si hay numerosas inserciones en la tabla, pero es una buena opción si los datos son estáticos o solo cambian con poca frecuencia. Si un almacén de columnas no es adecuado, se puede usar la compresión en una tabla principal de fila para mejorar la E/S.

Para obtener más información, vea los documentos siguientes:

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar la compresión en una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guía de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tablas con optimización para memoria

En la actualidad, la memoria ya no es un problema para los equipos modernos. A medida que las especificaciones de hardware continúan mejorando, es relativamente fácil obtener RAM en buenos valores. Sin embargo, al mismo tiempo, los datos se producen más rápidamente que nunca, y los datos se deben procesar con baja latencia.

Las tablas optimizadas para memoria representan una solución, ya que aprovechan la gran cantidad de memoria disponible en los equipos avanzados para abordar el problema de los macrodatos. Las tablas optimizadas para memoria residen principalmente en la memoria, por lo que los datos se leen y se escriben en la memoria. En cuanto a la durabilidad, se mantiene una segunda copia de la tabla en el disco y los datos solo se leen desde el disco durante la recuperación de la base de datos.

Si tiene que leer y escribir en las tablas con frecuencia, las tablas optimizadas para memoria pueden ayudar con una alta escalabilidad y una baja latencia.  En el escenario de búsqueda de coincidencias, el uso de tablas optimizadas para memoria nos permitió leer todas las características de reanudación de la base de datos y almacenarlas en la memoria principal para que coincidan con las nuevas aperturas de trabajo. Esto reduce considerablemente la e/s de disco.

Las mejoras de rendimiento adicionales se logran mediante el uso de una tabla optimizada para memoria en el proceso de escritura de predicciones en la base de datos desde varios lotes simultáneos. El uso de tablas optimizadas para memoria en SQL Server habilitada la latencia baja en las lecturas y escrituras de tabla.

La experiencia también era perfecta durante el desarrollo. Las tablas optimizadas para memoria perdurables se crearon al mismo tiempo que se creó la base de datos. Por lo tanto, el desarrollo usó el mismo flujo de trabajo, independientemente de dónde se almacenaron los datos.

### <a name="processor"></a>Procesador

SQL Server puede realizar tareas en paralelo mediante el uso de núcleos disponibles en el equipo; cuanto mayor sea el número de núcleos disponibles, mejor será el rendimiento. Aunque es posible que el aumento del número de núcleos no ayude en las operaciones enlazadas a e/s, los algoritmos enlazados a la CPU se benefician de las CPU más rápidas con muchos núcleos.

Dado que el servidor se utiliza normalmente por varios usuarios simultáneamente, el administrador de la base de datos debe determinar el número ideal de núcleos necesarios para admitir los cálculos de carga de trabajo máxima.

### <a name="resource-governance"></a>Gobernanza de recursos

En las ediciones que admiten Resource Governor, puede usar grupos de recursos para especificar que se asigne cierto número de CPU a ciertas cargas de trabajo. También puede administrar la cantidad de memoria asignada a cargas de trabajo específicas.

La regulación de recursos en SQL Server le permite centralizar la supervisión y el control de los distintos recursos utilizados por SQL Server y por R. Por ejemplo, podría asignar la mitad de la memoria disponible para el motor de base de datos para asegurarse de que los servicios principales siempre se pueden ejecutar a pesar de cargas de trabajo más pesadas transitorias.

El valor predeterminado para el consumo de memoria por parte de los scripts externos está limitado al 20% de la memoria total disponible para SQL Server. Este límite se aplica de forma predeterminada para asegurarse de que todas las tareas que se basan en el servidor de base de datos no se ven afectadas gravemente por trabajos de R de larga ejecución. Pero el administrador de bases de datos puede cambiar estos límites. En muchos casos, el límite del 20% no es adecuado para admitir cargas de trabajo de aprendizaje automático graves.

Las opciones de configuración admitidas son **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**y **MAX_PROCESSES**. Para ver la configuración actual, use esta instrucción:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  Si el servidor se usa principalmente para R Services, podría ser útil aumentar MAX_CPU_PERCENT a 40% o 60%.

-  Si muchas sesiones de R deben usar el mismo servidor al mismo tiempo, se deben aumentar los tres valores de configuración.

Para cambiar los valores de recursos asignados, use instrucciones T-SQL.

+ Esta instrucción establece el uso de memoria en 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Esta instrucción establece los tres valores configurables:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Si cambia la configuración de memoria, CPU o proceso máximo y desea aplicar la configuración inmediatamente, ejecute esta instrucción:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA, NUMA de hardware y afinidad de CPU

Cuando se usa SQL Server como el contexto de cálculo, a veces se puede lograr un mejor rendimiento al optimizar la configuración relacionada con NUMA y la afinidad del procesador. 

Los sistemas con _Numa de hardware_ tienen más de un bus de sistema y cada uno de ellos sirve a un pequeño conjunto de procesadores. Cada CPU puede tener acceso a la memoria asociada a otros grupos de forma coherente. Cada grupo se denomina nodo NUMA. Si tiene NUMA de hardware, lo puede configurar para que utilice memoria intercalada en vez de NUMA. En ese caso, Windows y, por lo tanto, SQL Server no lo reconocerá como NUMA. 

Puede ejecutar la consulta siguiente para buscar el número de nodos de memoria disponibles para SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Si la consulta devuelve un solo nodo de memoria (nodo 0), o bien no tiene NUMA de hardware o el hardware está configurado como intercalado (no NUMA). También SQL Server omite NUMA de hardware cuando hay cuatro CPU o menos, o si al menos un nodo tiene solo una CPU.

Si el equipo tiene varios procesadores pero no tiene hardware-NUMA, también puede usar [Soft-Numa](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) para subdividir las CPU en grupos más pequeños.  En SQL Server 2016 y SQL Server 2017, la característica de Soft-NUMA se habilita automáticamente al iniciar el servicio de SQL Server.

Cuando Soft-NUMA está habilitado, SQL Server administra automáticamente los nodos. sin embargo, para optimizar las cargas de trabajo específicas, puede deshabilitar la _afinidad de software_ y configurar manualmente la afinidad de la CPU para los nodos Numa de software. Esto puede proporcionarle más control sobre qué cargas de trabajo se asignan a los nodos, especialmente si usa una edición de SQL Server que admita la regulación de recursos. Al especificar la afinidad de la CPU y alinear los grupos de recursos con grupos de CPU, puede reducir la latencia y asegurarse de que los procesos relacionados se realizan en el mismo nodo NUMA.

El proceso general para configurar la afinidad de Soft-NUMA y CPU para admitir las cargas de trabajo de R es el siguiente:

1. Habilitación de Soft-NUMA, si está disponible
2. Definir la afinidad del procesador
3. Crear grupos de recursos para procesos externos con [Resource Governor](../r/resource-governance-for-r-services.md)
4. Asignación de [grupos de cargas de trabajo](../../relational-databases/resource-governor/resource-governor-workload-group.md) a grupos de afinidad específicos

Para obtener más información, incluido el código de ejemplo, consulte este tutorial: [Sugerencias y trucos para la optimización de SQL (ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Otros recursos:**

+ [Soft-NUMA en SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Cómo asignar nodos NUMA de software a las CPU

## <a name="task-specific-optimizations"></a>Optimizaciones específicas de tareas

En esta sección se resumen los métodos adoptados en estos casos prácticos y, en otras pruebas, para optimizar cargas de trabajo específicas de aprendizaje automático. Las cargas de trabajo comunes incluyen el entrenamiento del modelo, la extracción de características y la ingeniería de características, y varios escenarios de puntuación: una fila, un lote pequeño y un lote grande.

### <a name="feature-engineering"></a>Ingeniería de características

Un punto problemático con R es que normalmente se procesa en una sola CPU. Se trata de un cuello de botella de rendimiento importante para muchas tareas, especialmente la ingeniería de características. En la solución resume-Matching, la tarea de ingeniería de características creó solo 2.500 características entre productos que debían combinarse con las características 100 originales. Esta tarea tardaría bastante tiempo si todo se realizaba en una sola CPU.

Hay varias maneras de mejorar el rendimiento del diseño de características. Puede optimizar el código R y mantener la extracción de características en el proceso de modelado, o bien trasladar el proceso de ingeniería de características a SQL.

- Usar R. Puede definir una función y, a continuación, pasarla como argumento a [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante el entrenamiento. Si el modelo admite el procesamiento en paralelo, la tarea de ingeniería de características se puede procesar con varias CPU. Con este enfoque, el equipo de ciencia de datos observó una mejora del rendimiento del 16% en cuanto al tiempo de puntuación. Sin embargo, este enfoque requiere un modelo que admita la paralelización y una consulta que se pueda ejecutar mediante un plan paralelo.

- Use R con un contexto de cálculo de SQL. En un entorno de varios procesadores con recursos aislados disponibles para la ejecución de lotes independientes, se puede lograr una mayor eficacia al aislar las consultas SQL usadas en cada lote, extraer datos de las tablas y restringir los datos en el mismo grupo de cargas de trabajo. Los métodos que se usan para aislar los lotes incluyen la creación de particiones y el uso de PowerShell para ejecutar consultas independientes en paralelo.

- Ejecución en paralelo ad hoc: En un contexto de cálculo de SQL Server, puede basarse en el motor de base de datos SQL para aplicar la ejecución en paralelo, si es posible, y si esa opción es más eficaz.

- Use T-SQL en un proceso de características independiente. La de los datos de características con SQL suele ser más rápida.

### <a name="prediction-scoring-in-parallel"></a>Predicción (puntuación) en paralelo

Una de las ventajas de SQL Server es su capacidad para controlar un gran volumen de filas en paralelo. En ningún caso, se marca como en puntuación. Por lo general, el modelo no necesita tener acceso a todos los datos para su puntuación, por lo que puede crear particiones de los datos de entrada, con cada grupo de cargas de trabajo procesando una tarea.

También puede enviar los datos de entrada como una sola consulta y SQL Server después analiza la consulta. Si se puede crear un plan de consulta paralelo para los datos de entrada, particiona automáticamente los datos asignados a los nodos y realiza también las combinaciones y agregaciones necesarias en paralelo.

Si le interesan los detalles de cómo definir un procedimiento almacenado para usarlo en la puntuación, vea el proyecto de ejemplo en [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) y busque el archivo "step5_score_for_matching. SQL". El script de ejemplo también realiza el seguimiento de las horas de inicio y finalización de la consulta y escribe el tiempo en la consola de SQL para que pueda evaluar el rendimiento.

### <a name="concurrent-scoring-using-resource-groups"></a>Puntuación simultánea mediante grupos de recursos

Para escalar verticalmente el problema de puntuación, se recomienda adoptar el enfoque Map-reduce en el que millones de elementos se dividen en varios lotes. A continuación, se ejecutan varios trabajos de puntuación simultáneamente. En este marco, los lotes se procesan en diferentes conjuntos de CPU y los resultados se recopilan y se vuelven a escribir en la base de datos.

Este es el enfoque que se usa en el escenario de búsqueda de coincidencias. sin embargo, el gobierno de recursos en SQL Server es esencial para implementar este enfoque. Mediante la configuración de grupos de cargas de trabajo para trabajos de script externos, puede enrutar los trabajos de puntuación de R a distintos grupos de procesadores y lograr un rendimiento más rápido.

La regulación de recursos también puede ayudar a asignar los recursos disponibles en el servidor (CPU y memoria) para minimizar la competencia de la carga de trabajo. Puede configurar funciones clasificadoras para distinguir entre diferentes tipos de trabajos de R: por ejemplo, puede decidir que la puntuación a la que se llama desde una aplicación siempre tiene prioridad, mientras que los trabajos de reentrenamiento tienen una prioridad baja. Este aislamiento de recursos puede mejorar el tiempo de ejecución y proporcionar un rendimiento más predecible.

### <a name="concurrent-scoring-using-powershell"></a>Puntuación simultánea mediante PowerShell

Si decide particionar los datos usted mismo, puede usar scripts de PowerShell para ejecutar varias tareas de puntuación simultáneas. Para ello, use el cmdlet Invoke-SqlCmd e inicie las tareas de puntuación en paralelo.

En el escenario de búsqueda de coincidencias, la simultaneidad se diseñó del modo siguiente:

- 20 procesadores divididos en cuatro grupos de cinco CPU cada uno. Cada grupo de CPU se encuentra en el mismo nodo NUMA.

- El número máximo de lotes simultáneos se estableció en ocho.

- Cada grupo de cargas de trabajo debe administrar dos tareas de puntuación. En cuanto una tarea termina de leer los datos y comienza la puntuación, la otra tarea puede empezar a leer los datos de la base de datos.

Para ver los scripts de PowerShell para este escenario, abra el archivo experimento. PS1 en el [proyecto de github](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Almacenar modelos para la predicción

Cuando finaliza el entrenamiento y la evaluación y se selecciona un modelo mejor, se recomienda almacenar el modelo en la base de datos para que esté disponible para las predicciones. Cargar el modelo precalculado de la base de datos para la predicción es eficaz, ya que SQL Server machine learning usa algoritmos de serialización especiales para almacenar y cargar modelos cuando se mueve entre R y la base de datos.

> [!TIP]
> En SQL Server 2017, puede usar la función PREDICT para realizar la puntuación aunque R no esté instalado en el servidor. Se admiten los tipos de modelos limitados, del paquete RevoScaleR.

Sin embargo, dependiendo del algoritmo que utilice, algunos modelos pueden ser bastante grandes, especialmente cuando se entrenan en un conjunto de datos grande. Por ejemplo, los algoritmos como **LM** o **GLM** generan muchos datos de Resumen junto con las reglas. Dado que hay límites en el tamaño de un modelo que se puede almacenar en una columna varbinary, se recomienda eliminar los artefactos innecesarios del modelo antes de almacenar el modelo en la base de datos para producción.

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Optimización del rendimiento para R: introducción](../r/sql-server-r-services-performance-tuning.md)

[Ajuste del rendimiento para la configuración de R-SQL Server](../r/sql-server-configuration-r-services.md)

[Optimización del rendimiento de código R-R y optimización de datos](../r/r-and-data-optimization-r-services.md)

[Optimización del rendimiento: resultados de los casos prácticos](../r/performance-case-study-r-services.md)
