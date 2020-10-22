---
title: Configuración para su uso con R
description: En este artículo se proporcionan instrucciones sobre la configuración de hardware y de red del equipo usado para ejecutar SQL Server R Services.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: feaa53fa47591ecdb3f1f0bc66ab390def8fbbb1
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195779"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuración de SQL Server para su uso con R
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artículo es el segundo de una serie de cuatro artículos en los que se describe la optimización del rendimiento de R Services, en función de dos casos prácticos.  En este artículo se proporcionan instrucciones sobre la configuración de hardware y de red del equipo que se usa para ejecutar SQL Server R Services. También contiene información sobre las formas de configurar la instancia, la base de datos o las tablas de SQL Server que se usarán en una solución. Dado que el uso de NUMA en SQL Server disipa la línea entre optimizaciones de hardware y de base de datos, en una tercera sección se describe detalladamente cómo lograr la afinidad de CPU y la regulación de recursos.

> [!TIP]
> Si no está familiarizado con SQL Server, le recomendamos encarecidamente que revise también la guía de optimización del rendimiento de SQL Server: [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)

## <a name="hardware-optimization"></a>Optimización de hardware

La optimización del equipo servidor es importante para asegurarse de que tiene los recursos necesarios para ejecutar scripts externos. Cuando los recursos están limitados, se pueden apreciar síntomas como los siguientes:

- La ejecución de trabajos se aplaza o se cancela para dar prioridad a otras operaciones de base de datos.
- Aparece el error "Se ha excedido la cuota" que hace que el script de R finalice sin acabar.
- Los datos cargados en la memoria de R se truncan y los resultados son incompletos.

### <a name="memory"></a>Memoria

La cantidad de memoria disponible en el equipo puede afectar considerablemente al rendimiento de los algoritmos de análisis avanzado. La memoria insuficiente podría afectar al grado de paralelismo cuando se usa el contexto de cálculo de SQL. También puede afectar al tamaño de los fragmentos (filas por operación de lectura) que se puede procesar y al número de sesiones simultáneas que se admiten.

Se recomienda encarecidamente un mínimo de 32 GB. Si tiene disponibles más de 32 GB, puede configurar el origen de datos de SQL para que use más filas en cada operación de lectura y, así, mejorar el rendimiento.

También puede administrar la memoria que la instancia usa. Cuando se asigna memoria, SQL Server tiene prioridad de forma predeterminada frente a los procesos de script externos. En una instalación predeterminada de R Services, solo se asigna un 20 % de la memoria disponible a R.

Por lo general, esto no es suficiente para las tareas de ciencia de datos, pero tampoco conviene privar de memoria a SQL Server. Así pues, deberá experimentar y ajustar la asignación de memoria entre el motor de base de datos, los servicios relacionados y los scripts externos, sabiendo que la configuración óptima varía de un caso a otro.

En el modelo de búsqueda de CV, el uso de scripts externos era intenso y no se ejecutaba ningún otro servicio de motor de base de datos; por lo tanto, los recursos asignados a los scripts externos llegaron al 70 %, que era la mejor configuración para el rendimiento del script.

### <a name="power-options"></a>Opciones energía

En el sistema operativo Windows, debe usarse la opción de energía **Alto rendimiento**. El uso de una configuración de energía diferente provocará un rendimiento incoherente o reducido cuando se use SQL Server.

### <a name="disk-io"></a>E/S de disco

Los trabajos de entrenamiento y predicción mediante R Services están intrínsecamente enlazados a E/S, y dependen de la velocidad de los discos en los que la base de datos está almacenada. Las unidades de disco más rápidas, como las unidades de estado sólido (SSD), pueden ser de ayuda.

La E/S de disco también se ve afectada por otras aplicaciones que obtienen acceso al disco, por ejemplo, las operaciones de lectura en una base de datos mediante otros clientes. El rendimiento de E/S de disco también se puede ver afectado por la configuración del sistema de archivos que se use, como el tamaño de bloque usado por el sistema de archivos.

Si hay varias unidades disponibles, almacene las bases de datos en una unidad distinta de SQL Server para que las solicitudes relativas al motor de base de datos no lleguen al mismo disco que las solicitudes relativas a los datos almacenados en la base de datos.

La E/S de disco también puede afectar considerablemente al rendimiento cuando se ejecutan funciones analíticas RevoScaleR que usan varias iteraciones durante el entrenamiento. Por ejemplo, `rxLogit`, `rxDTree`, `rxDForest` y `rxBTrees` usan varias iteraciones. Cuando el origen de datos es SQL Server, estos algoritmos usan archivos temporales optimizados para capturar los datos. Estos archivos se limpian automáticamente una vez finalizada la sesión. Tener un disco de alto rendimiento para las operaciones de lectura y escritura puede mejorar significativamente el tiempo global transcurrido en estos algoritmos.

> [!NOTE]
> Las primeras versiones de R Services requerían compatibilidad con los nombres de archivo 8.3 en los sistemas operativos Windows. Esta restricción acabó con el Service Pack 1. Aun así, puede usar fsutil.exe para determinar si una unidad admite nombres de archivo 8.3 o para habilitar la compatibilidad en caso contrario.

### <a name="paging-file"></a>Archivo de paginación

El sistema operativo Windows usa un archivo de paginación para administrar los volcados de memoria y para almacenar páginas de memoria virtual. Si observa una paginación excesiva, considere la posibilidad de aumentar la memoria física del equipo. Aunque el hecho de tener más memoria física no elimina la paginación, reduce la necesidad de paginación.

La velocidad del disco en el que se almacena el archivo de paginación también puede afectar al rendimiento. Si se almacena el archivo de paginación en un SSD o si se usan varios archivos de paginación en varios SSD, puede mejorar el rendimiento.

Para más información sobre el ajuste de tamaño del archivo de paginación, vea [Determinar el tamaño apropiado del archivo de paginación para las versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Optimizaciones en el nivel de instancia o de base de datos

La optimización de la instancia de SQL Server es la clave para lograr una ejecución eficaz de los scripts externos.

> [!NOTE]
> La configuración óptima varía en función del tamaño y del tipo de los datos y del número de columnas que se usa para puntuar o entrenar un modelo.
> 
> Puede revisar los resultados de las optimizaciones específicas en el artículo final: [Optimización del rendimiento: resultados de casos prácticos](../../machine-learning/r/performance-case-study-r-services.md)
> 
> Para obtener scripts de ejemplo, vea el [repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) independiente.

### <a name="table-compression"></a>Compresión de tabla

A menudo, el rendimiento de E/S se puede mejorar usando la compresión o un almacén de datos en forma de columna. Por lo general, los datos se suelen repetir en varias columnas de una tabla, por lo que el uso de un almacén de columnas aprovecha estas repeticiones al comprimir los datos.

Un almacén de columnas podría no ser muy eficaz si hay una gran cantidad de inserciones en la tabla, pero es una buena opción si los datos son estáticos o si cambian con poca frecuencia. Si un almacén de columnas no es adecuado, se puede usar la compresión en una tabla principal de fila para mejorar la E/S.

Para obtener más información, vea los documentos siguientes:

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guía de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tablas optimizadas para memoria

En la actualidad, la memoria de los equipos modernos ha dejado de ser un problema. A medida que las especificaciones de hardware siguen mejorando, es relativamente fácil obtener buenas capacidades de RAM. Sin embargo, al mismo tiempo se generan datos más rápidamente que nunca, y estos datos se deben procesar con una latencia baja.

Las tablas optimizadas para memoria constituyen una solución, ya que aprovechan la gran cantidad de memoria disponible en los equipos avanzados para abordar el problema de los macrodatos. Las tablas optimizadas para memoria residen principalmente en la memoria, de forma que los datos se leen y se escriben en la memoria. En cuanto a la durabilidad, se mantiene una segunda copia de la tabla en el disco, y los datos solo se leen desde el disco durante una recuperación de la base de datos.

Si tiene que leer y escribir en las tablas con frecuencia, las tablas optimizadas para memoria pueden ayudar con una alta escalabilidad y una baja latencia.  En el escenario de búsqueda de CV, el uso de tablas optimizadas para memoria nos permitió leer todas las características de los CV de la base de datos y almacenarlas en la memoria principal para contrastarlas con las ofertas de trabajo nuevas. Esto redujo notablemente la E/S de disco.

También se lograron otras mejoras de rendimiento mediante el uso de una tabla optimizada para memoria en el proceso de escritura de predicciones en la base de datos desde varios lotes simultáneos. El uso de tablas optimizadas para memoria en SQL Server permitió una latencia baja en las lecturas y escrituras de tabla.

La experiencia también fue perfecta durante el desarrollo. Se crearon tablas optimizadas para memoria perdurables al mismo tiempo que la base de datos, de modo que en el desarrollo se usó el mismo flujo de trabajo, independientemente de dónde estuvieran almacenados los datos.

### <a name="processor"></a>Procesador

SQL Server puede realizar tareas en paralelo mediante el uso de los núcleos disponibles en el equipo. Cuantos más núcleos haya disponibles, mejor será el rendimiento. Aunque aumentar el número de núcleos no ayude en las operaciones enlazadas a E/S, los algoritmos enlazados a CPU saldrán beneficiados si las CPU son más rápidas y tienen varios núcleos.

Dado que lo habitual es que varios usuarios usen el servidor simultáneamente, el administrador de bases de datos debe determinar el número ideal de núcleos que se necesitan para admitir cálculos de carga de trabajo máxima.

### <a name="resource-governance"></a>Regulación de recursos

En las ediciones que admiten Resource Governor, se pueden usar grupos de recursos para especificar que se asigne un número determinado de CPU a cargas de trabajo específicas. También se puede administrar la cantidad de memoria asignada a cargas de trabajo específicas.

La regulación de recursos en SQL Server permite centralizar la supervisión y el control de los distintos recursos utilizados por SQL Server y por R. Por ejemplo, podría asignar la mitad de la memoria disponible al motor de base de datos para asegurarse de que los servicios principales siempre puedan ejecutarse a pesar de las cargas de trabajo más pesadas transitorias.

El valor predeterminado de consumo de memoria de los scripts externos se limita al 20 % de la memoria total disponible para SQL Server. Este límite se aplica de forma predeterminada para procurar que todas las tareas basadas en el servidor de base de datos no se vean afectadas en gran medida por los trabajos de R de larga duración. Pero el administrador de bases de datos puede cambiar estos límites. En muchos casos, el límite del 20 % no es adecuado para admitir cargas de trabajo de Machine Learning de cierta magnitud.

Las opciones de configuración admitidas son **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT** y **MAX_PROCESSES**. Para ver la configuración actual, use esta instrucción: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Si el servidor se usa principalmente para R Services, puede resultar útil aumentar MAX_CPU_PERCENT hasta el 40 % o el 60 %.

-  Si muchas sesiones de R deben usar el mismo servidor al mismo tiempo, se deben aumentar las tres opciones de configuración.

Para cambiar los valores de los recursos asignados, use instrucciones T-SQL.

+ En esta instrucción se establece el uso de memoria en un 40 %: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ En esta instrucción se establecen los tres valores configurables: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Si cambia la configuración de memoria, de CPU o de proceso máximo y quiere aplicar dicha configuración inmediatamente, ejecute esta instrucción: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA, NUMA de hardware y afinidad de CPU

Cuando SQL Server se usa como el contexto de cálculo, a veces se puede lograr un mejor rendimiento si se optimiza la configuración relacionada con NUMA y la afinidad del procesador. 

Los sistemas con _NUMA de hardware_ disponen de más de un bus del sistema, y cada uno de ellos sirve a un pequeño conjunto de procesadores. Cada CPU puede acceder a la memoria asociada a otros grupos de forma coherente. Cada grupo se denomina nodo NUMA. Si tiene NUMA de hardware, lo puede configurar para que utilice memoria intercalada en vez de NUMA. En ese caso, Windows (y, por tanto, SQL Server) no lo reconocerá como NUMA. 

Puede ejecutar la siguiente consulta para conocer el número de nodos de memoria disponibles para SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Si la consultar devuelve solamente un único nodo de memoria (nodo 0), significará que no dispone de NUMA de hardware, o que el hardware está configurado como intercalado (no NUMA). SQL Server omite el NUMA de hardware también cuando hay cuatro CPU o menos, o si al menos un nodo tiene una sola CPU.

Si el equipo tiene varios procesadores, pero no tiene hardware de NUMA, también puede usar [Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) para subdividir las CPU en grupos más pequeños.  En SQL Server 2016 y SQL Server 2017, la característica Soft-NUMA se habilita automáticamente al iniciar el servicio de SQL Server.

Cuando Soft-NUMA está habilitado, SQL Server administra los nodos automáticamente; sin embargo, para optimizar cargas de trabajo específicas, puede deshabilitar la _afinidad flexible_ y configurar manualmente la afinidad de la CPU de los nodos de Soft-NUMA. Esto le reportará un mayor control sobre qué cargas de trabajo se asignan a los nodos, especialmente si usa una edición de SQL Server que admite la regulación de recursos. Al especificar la afinidad de la CPU y alinear los grupos de recursos con grupos de CPU, puede reducir la latencia y asegurarse de que los procesos relacionados se realizan en el mismo nodo NUMA.

Este es el proceso general para configurar Soft-NUMA y la afinidad de CPU para admitir las cargas de trabajo de R:

1. Habilitar Soft-NUMA, si está disponible
2. Definir la afinidad del procesador
3. Crear grupos de recursos para procesos externos mediante [Resource Governor](../administration/resource-governor.md)
4. Asignar los [grupos de cargas de trabajo](../../relational-databases/resource-governor/resource-governor-workload-group.md) a grupos de afinidad específicos

Para más información, incluido código de ejemplo, vea este tutorial: [Sugerencias y trucos para la optimización de SQL (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Otros recursos:**

+ [Soft-NUMA en SQL Server](../../database-engine/configure-windows/soft-numa-sql-server.md)
    
    Cómo asignar nodos de Soft-NUMA a las CPU

## <a name="task-specific-optimizations"></a>Optimizaciones específicas de tareas

En esta sección se resumen los métodos adoptados en estos casos prácticos (y en otras pruebas) para optimizar cargas de trabajo de Machine Learning específicas. Las cargas de trabajo comunes incluyen el entrenamiento del modelo, la extracción de características y la ingeniería de características, así como varios escenarios de puntuación: por fila, por lote pequeño y por lote grande.

### <a name="feature-engineering"></a>Ingeniería de características

Un punto débil de R es que se suele procesar en una sola CPU, lo que constituye un cuello de botella de rendimiento importante en muchas tareas, especialmente en la ingeniería de características. En la solución de búsqueda de CV, solo la tarea de ingeniería de características creó 2500 características entre productos que debían combinarse con las 100 características originales. Esta tarea tardaría bastante tiempo si todo se realizara en una sola CPU.

Existen varias maneras de mejorar el rendimiento de la ingeniería de características. Se puede optimizar el código de R y mantener la extracción de características dentro del proceso de modelado, o bien trasladar el proceso de ingeniería de características a SQL.

- Usar R. Se define una función y, después, se pasa como argumento a [rxTransform](/r-server/r-reference/revoscaler/rxtransform) durante el entrenamiento. Si el modelo admite el procesamiento en paralelo, la tarea de ingeniería de características se puede procesar con varias CPU. Con este método, el equipo de ciencia de datos observó una mejora del rendimiento del 16 % en cuanto a tiempo de puntuación, pero se necesita un modelo que admita la paralelización y una consulta que se pueda ejecutar mediante un plan paralelo.

- Usar R con un contexto de cálculo de SQL. En un entorno de varios procesadores con recursos aislados disponibles para la ejecución de lotes independientes, se puede lograr una mayor eficacia si se aíslan las consultas SQL usadas en cada lote para extraer datos de las tablas y restringir los datos en el mismo grupo de cargas de trabajo. Los métodos que se usan para aislar los lotes incluyen la creación de particiones y el uso de PowerShell para ejecutar consultas independientes en paralelo.

- Ejecución en paralelo ad hoc. En un contexto de cálculo de SQL Server, se puede basar en el motor de base de datos de SQL para aplicar la ejecución en paralelo, si es posible y si esa opción es más eficaz.

- Usar T-SQL en un proceso de características independiente. Precalcular los datos de características con SQL suele ser más rápido.

### <a name="prediction-scoring-in-parallel"></a>Predicción (puntuación) en paralelo

Una de las ventajas de SQL Server es su capacidad para controlar un gran volumen de filas en paralelo, y el ámbito donde esta ventaja se hace más patente es en la puntuación. Por lo general, el modelo no necesita acceder a todos los datos para la puntuación, por lo que puede crear particiones de los datos de entrada, encargándose cada grupo de cargas de trabajo de procesar una tarea.

También puede enviar los datos de entrada como una sola consulta, que SQL Server analiza. Si se puede elaborar un plan de consulta paralelo para los datos de entrada, se crean particiones de los datos asignados a los nodos automáticamente, y se llevan a cabo también las combinaciones y agregaciones necesarias en paralelo.

Si le interesa obtener información detallada sobre cómo definir un procedimiento almacenado para usarlo en la puntuación, vea el proyecto de ejemplo en [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching/SQLR) y busque el archivo "step5_score_for_matching.sql". El script de ejemplo también lleva un seguimiento de las horas de inicio y de fin de la consulta, y registra el tiempo en la consola de SQL para que pueda evaluar el rendimiento.

### <a name="concurrent-scoring-using-resource-groups"></a>Puntuación simultánea mediante grupos de recursos

Para escalar verticalmente el problema de puntuación, se recomienda adoptar el método de asignación y reducción, por el que millones de elementos se dividen en varios lotes. Tras ello, se ejecutan varios trabajos de puntuación simultáneamente. En este marco, los lotes se procesan en diferentes conjuntos de CPU, y los resultados se recopilan y se vuelven a escribir en la base de datos.

Este es el método empleado en el escenario de búsqueda de CV, si bien para ponerlo en marcha es fundamental disponer de la regulación de recursos en SQL Server. Al configurar grupos de cargas de trabajo para trabajos de script externos, los trabajos de puntuación de R se pueden enrutar a distintos grupos de procesadores y lograr un rendimiento más rápido.

La regulación de recursos también puede ayudar a asignar los recursos disponibles en el servidor (CPU y memoria) para minimizar la competición de cargas de trabajo. Puede configurar funciones de clasificación para distinguir entre diferentes tipos de trabajos de R; por ejemplo, puede decidir que la puntuación a la que se llama desde una aplicación tenga siempre prioridad, mientras que los trabajos de reciclaje tengan una prioridad baja. Este aislamiento de recursos puede mejorar en teoría el tiempo de ejecución y alcanzar un rendimiento más predecible.

### <a name="concurrent-scoring-using-powershell"></a>Puntuación simultánea con PowerShell

Si decide crear particiones de los datos por sí mismo, puede usar scripts de PowerShell para ejecutar varias tareas de puntuación a la vez. Para ello, use el cmdlet Invoke-SqlCmd e inicie las tareas de puntuación en paralelo.

En el escenario de búsqueda de CV, la simultaneidad se diseñó del siguiente modo:

- 20 procesadores divididos entre cuatro grupos de cinco CPU cada uno. Cada grupo de CPU se encuentra en el mismo nodo NUMA.

- El número máximo de lotes simultáneos se estableció en ocho.

- Cada grupo de cargas de trabajo debe encargarse de dos tareas de puntuación. En cuanto una tarea termine de leer los datos y la puntuación se inicia, la otra puede empezar a leer datos de la base de datos.

Para ver los scripts de PowerShell de este escenario, abra el archivo experiment.ps1 del [proyecto de Github](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching).

### <a name="storing-models-for-prediction"></a>Almacenamiento de modelos para la predicción

Cuando el entrenamiento y la evaluación terminen y haya seleccionado el mejor modelo, se recomienda almacenar el modelo en la base de datos para que esté disponible para las predicciones. Cargar el modelo precalculado desde la base de datos para la predicción es eficaz, ya que SQL Server Machine Learning usa algoritmos de serialización especiales para almacenar y cargar modelos cuando se alterna entre R y la base de datos.

> [!TIP]
> En SQL Server 2017, puede usar la función PREDICT para realizar la puntuación, aunque R no esté instalado en el servidor. Se admiten ciertos tipos de modelos limitados del paquete RevoScaleR.

Sin embargo, dependiendo del algoritmo que use, algunos modelos pueden ser bastante grandes, especialmente cuando se entrenan en un conjunto de datos grande. Por ejemplo, algoritmos como **lm** o **glm** generan muchos datos de resumen, aparte de reglas. Dado que hay límites en el tamaño de un modelo que se puede almacenar en una columna varbinary, se recomienda eliminar los artefactos innecesarios del modelo antes de almacenarlo en la base de datos para producción.

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Optimización del rendimiento de R: introducción](../r/sql-server-r-services-performance-tuning.md)

[Optimización del rendimiento de R: configuración de SQL Server](../r/sql-server-configuration-r-services.md)

[Optimización del rendimiento de R: optimización de datos y de código de R](../r/r-and-data-optimization-r-services.md)

[Optimización del rendimiento: resultados de casos prácticos](../r/performance-case-study-r-services.md)