---
title: 'Configuración de SQL Server (R Services): SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 9ad4d1a23a05db35e0c4b55473903dbf7e4265da
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645547"
---
# <a name="sql-server-configuration-for-use-with-r"></a>Configuración de SQL Server para su uso con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo es el segundo de una serie que se describe la optimización del rendimiento para servicios de R según dos casos prácticos.  Este artículo proporcionan instrucciones sobre la configuración de hardware y de red del equipo que se usa para ejecutar SQL Server R Services. También contiene información acerca de las formas de configurar la instancia de SQL Server, base de datos o las tablas usadas en una solución. Dado que el uso de NUMA en SQL Server difumina las líneas entre las optimizaciones de hardware y la base de datos, una tercera sección describe CPU afinamiento y regulación de recursos en detalle.

> [!TIP]
> Si está familiarizado con SQL Server, se recomienda encarecidamente que revise también la Guía de optimización del rendimiento de SQL Server: [Supervisión y optimización del rendimiento](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance).

## <a name="hardware-optimization"></a>Optimización del hardware

Optimización del equipo del servidor es importante para asegurarse de que tiene los recursos necesarios para ejecutar scripts externos. Cuando los recursos son limitados, puede aparecer síntomas, como los siguientes:

- Ejecución del trabajo se aplaza o cancele para dar prioridad a otras operaciones de base de datos
- Script de R que producen error "ha excedido la cuota" para finalizar sin finalización
- Datos cargados en memoria de R que se trunca, de resultados incompletos

### <a name="memory"></a>Memoria

La cantidad de memoria disponible en el equipo puede afectar considerablemente al rendimiento de los algoritmos de análisis avanzado. Memoria insuficiente puede afectar al grado de paralelismo cuando se usa el contexto de cálculo SQL. También puede afectar al tamaño de los fragmentos (filas por operación de lectura) que se puede procesar y al número de sesiones simultáneas que se admiten.

Se recomienda un mínimo de 32 GB. Si tiene más de 32 GB de espacio disponible, puede configurar el origen de datos SQL para que use más filas en cada operación de lectura para mejorar el rendimiento.

También puede administrar la memoria utilizada por la instancia. De forma predeterminada, SQL Server se prioriza sobre los procesos de script externo cuando se asigna memoria. En una instalación predeterminada de R Services, solo el 20% de memoria disponible se asigna a R.

Normalmente, esto no es suficiente para tareas de ciencia de datos, pero tampoco es conveniente que se agote el servidor SQL server de la memoria. Debe experimentar y ajustar la asignación de memoria entre el motor de base de datos y servicios relacionados scripts externos, teniendo en cuenta que la configuración óptima varía caso por caso.

Para el modelo de coincidencia de reanudar el uso de scripts externos estaba pesado y no había ninguna base de datos de otro servicios de motor de ejecución; por lo tanto, los recursos asignados a los scripts externos se han aumentado al 70%, lo que era la mejor configuración para el rendimiento de la secuencia de comandos.

### <a name="power-options"></a>Opciones energía

En el sistema operativo Windows, el **de alto rendimiento** se debe usar la opción de energía. Mediante la configuración de energía diferente da como resultado un rendimiento incoherente o reducido cuando se usa SQL Server.

### <a name="disk-io"></a>E/S de disco

Entrenamiento y predicción trabajos con R Services son inherentemente E/S enlazan y dependen de la velocidad de los discos almacenados en la base de datos. Pueden ayudar las unidades más rápidas, como unidades de estado sólido (SSD).

La E/S de disco también se ve afectada por otras aplicaciones que obtienen acceso al disco, por ejemplo, las operaciones de lectura en una base de datos mediante otros clientes. El rendimiento de E/S de disco también se puede ver afectado por la configuración del sistema de archivos que se use, como el tamaño de bloque usado por el sistema de archivos.

Si hay varias unidades, almacén de las bases de datos en una unidad distinta de SQL Server de forma que las solicitudes para el motor de base de datos que no han alcanzado el mismo disco que las solicitudes de datos almacenados en la base de datos.

La E/S de disco también puede afectar considerablemente al rendimiento cuando se ejecutan funciones analíticas RevoScaleR que usan varias iteraciones durante el entrenamiento. Por ejemplo, `rxLogit`, `rxDTree`, `rxDForest`, y `rxBTrees` usan varias iteraciones. Cuando el origen de datos es SQL Server, estos algoritmos usan archivos temporales que se optimizan para capturar los datos. Estos archivos se limpian automáticamente una vez finalizada la sesión. Tener un disco de alto rendimiento para las operaciones de lectura/escritura puede mejorar significativamente el tiempo global transcurrido para estos algoritmos.

> [!NOTE]
> Las versiones anteriores de R Services requieren la compatibilidad con nombre de archivo 8.3 en sistemas operativos de Windows. Esta restricción se soluciona después de Service Pack 1. Sin embargo, puede usar fsutil.exe para determinar si una unidad admite nombres de 8.3 archivo o para habilitar la compatibilidad si no es así.

### <a name="paging-file"></a>Archivo de paginación

El sistema operativo Windows usa un archivo de paginación para administrar los volcados de memoria y para almacenar páginas de memoria virtual. Si observa una paginación excesiva, considere la posibilidad de aumentar la memoria física del equipo. Aunque el hecho de tener más memoria física no elimina la paginación, reduce la necesidad de paginación.

La velocidad del disco en el que se almacena el archivo de paginación también puede afectar al rendimiento. Si se almacena el archivo de paginación en un SSD o si se usan varios archivos de paginación en varios SSD, puede mejorar el rendimiento.

Para obtener información sobre el tamaño del archivo de paginación, vea [cómo determinar el tamaño del archivo de página adecuado para versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880).

## <a name="optimizations-at-instance-or-database-level"></a>Optimizaciones a nivel de instancia o base de datos

Optimización de la instancia de SQL Server es la clave para una ejecución eficaz de scripts externos.

> [!NOTE]
> Los valores óptimos varían según el tamaño y tipo de los datos, el número de columnas que se usa para la puntuación o entrenar un modelo.
> 
> Puede revisar los resultados de las optimizaciones específicas en el artículo final: [Los resultados del caso práctico: optimización del rendimiento](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> Para scripts de muestra, vea el separar [repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

### <a name="table-compression"></a>Compresión de tabla

A menudo se puede mejorar el rendimiento de E/S mediante compresión o un almacén de datos en columnas. Por lo general, los datos a menudo se repiten en varias columnas de una tabla, por lo que usar un almacén de columnas aprovecha estas repeticiones al comprimir los datos.

Un almacén de columnas podría no ser tan eficaz si hay muchas inserciones en la tabla, pero es una buena opción si los datos son estáticos o solo cambian con poca frecuencia. Si un almacén de columnas no es adecuado, se puede usar la compresión en una tabla principal de fila para mejorar la E/S.

Para obtener más información, vea los documentos siguientes:

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar la compresión en una tabla o índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Guía de índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>Tablas con optimización para memoria

En la actualidad, la memoria ya no es un problema para los equipos modernos. Como seguirán mejorando las especificaciones de hardware, es relativamente fácil de obtener memoria RAM en los valores correctos. Sin embargo, al mismo tiempo, se produce más rápidamente que nunca datos y se deben procesar los datos con una latencia baja.

Las tablas optimizadas para memoria representan una solución en que aprovechan la gran cantidad de memoria disponible en los equipos avanzados para abordar el problema de big data. Las tablas optimizadas para memoria principalmente residen en memoria, para que los datos se leen y escritos en la memoria. Para la durabilidad, una segunda copia de la tabla se mantiene en el disco y los datos solo se leen desde el disco durante la recuperación de base de datos.

Si tiene que leer y escribir en las tablas con frecuencia, las tablas optimizadas para memoria pueden ayudarle con alta escalabilidad y baja latencia.  En el escenario de coincidencia de reanudación, permite el uso de las tablas optimizadas para memoria nos permite leer todas las características de la reanudación de la base de datos y almacenarlos en la memoria principal, para que coincidan con nuevas ofertas de trabajo. Esto reduce considerablemente el E/S de disco.

Mejoras adicionales del rendimiento se lograban mediante el uso de la tabla optimizada para memoria en el proceso de escritura diferida de predicciones a la base de datos de varios lotes simultáneos. El uso de las tablas optimizadas en memoria en SQL Server había habilitada una latencia baja en la tabla lecturas y escrituras.

La experiencia también era transparente durante el desarrollo. Las tablas optimizadas en memoria perdurables se crearon al mismo tiempo que se creó la base de datos. Por lo tanto, desarrollo utiliza el mismo flujo de trabajo, independientemente de dónde se almacenan los datos.

### <a name="processor"></a>Procesador

SQL Server puede realizar tareas en paralelo con los núcleos disponibles en el equipo; más núcleos que están disponibles, mejor será el rendimiento. Aunque aumentar el número de núcleos podría no servir para operaciones de E/S enlazado, relacionadas con la CPU ventaja de los algoritmos de CPU más rápidas con el número de núcleos.

Dado que el servidor se usa normalmente por varios usuarios simultáneamente, el Administrador de base de datos debe determinar el número ideal de núcleos que se necesitan para admitir cálculos de carga de trabajo máxima.

### <a name="resource-governance"></a>Regulación de recursos

En las ediciones que admiten el regulador de recursos, puede usar los grupos de recursos para especificar que ciertas cargas de trabajo se asignan a un número de CPU. También puede administrar la cantidad de memoria asignada a cargas de trabajo específicas.

Regulación de recursos en SQL Server le permite centralizar la supervisión y control de los distintos recursos usada por SQL Server y R. Por ejemplo, podría asignar la mitad de la memoria disponible para el motor de base de datos, para asegurarse de que core servicios siempre pueden ejecutarse a pesar de las cargas de trabajo más pesadas transitorios.

El valor predeterminado para el consumo de memoria por scripts externos se limita a 20% de la memoria total disponible para su propio SQL Server. Este límite se aplica de forma predeterminada para asegurarse de que todas las tareas que se basan en el servidor de base de datos no se ve muy afectadas por los trabajos de R de larga ejecución. Pero el administrador de bases de datos puede cambiar estos límites. En muchos casos, el límite de 20% no es suficiente para admitir las cargas de trabajo de aprendizaje de automático grave.

Las opciones de configuración admitidas son **MAX_CPU_PERCENT**, **MAX_MEMORY_PERCENT**, y **MAX_PROCESSES**. Para ver la configuración actual, use esta instrucción: `SELECT * FROM sys.resource_governor_external_resource_pools`

-  Si el servidor se utiliza principalmente para R Services, puede resultar útil aumentar MAX_CPU_PERCENT hasta un 40% o el 60%.

-  Si muchas sesiones de R deben usar el mismo servidor al mismo tiempo, se deben incrementar las tres opciones.

Para cambiar los valores de los recursos asignados, use las instrucciones de T-SQL.

+ Esta instrucción establece el uso de memoria en un 40%: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ Esta instrucción establece los tres valores configurables: `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ Si cambia una configuración de proceso máximo, CPU o memoria y, a continuación, deberá aplicar la configuración inmediatamente, ejecute esta instrucción: `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Afinidad de CPU, NUMA de hardware y NUMA de software

Cuando se usa SQL Server como el contexto de cálculo, en ocasiones, puede lograr un mejor rendimiento ajustando la configuración relacionada con la afinidad del procesador y de NUMA. 

Los sistemas con _NUMA de hardware_ tiene más de un bus del sistema, que actúa un pequeño conjunto de procesadores. Cada CPU puede tener acceso a la memoria asociada a otros grupos de forma coherente. Cada grupo se denomina nodo NUMA. Si tiene NUMA de hardware, lo puede configurar para que utilice memoria intercalada en vez de NUMA. En ese caso, Windows y, por lo tanto, SQL Server lo no reconocerán como NUMA. 

Puede ejecutar la consulta siguiente para buscar el número de nodos de memoria disponibles para SQL Server:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

Si la consulta devuelve un único nodo de memoria (nodo 0), no dispone de NUMA de hardware o el hardware está configurado como intercalado (no NUMA). SQL Server también omite el hardware NUMA cuando hay cuatro o menos CPU, o si al menos un nodo tiene únicamente una CPU.

Si el equipo tiene varios procesadores, pero no tiene NUMA de hardware, también puede usar [Soft-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server) para subdividir las CPU en grupos más pequeños.  En SQL Server 2016 y SQL Server 2017, la característica de Soft-NUMA se habilita automáticamente al iniciar el servicio de SQL Server.

Cuando se habilita Soft-NUMA, SQL Server administra automáticamente los nodos para usted. Sin embargo, para optimizar cargas de trabajo específicas, puede deshabilitar _afinidad parcial_ y configurar manualmente la afinidad de CPU para los nodos NUMA de software. Esto puede proporcionarle más control sobre el que se asignan las cargas de trabajo a otros nodos, especialmente si está utilizando una edición de SQL Server que admite la regulación de recursos. Al especificar la afinidad de CPU y alineación de grupos de recursos con grupos de CPU, puede reducir la latencia y garantizar que los procesos relacionados se realizan en el mismo nodo NUMA.

El proceso general para configurar NUMA de software y la afinidad de CPU para admitir cargas de trabajo de R es el siguiente:

1. Habilitar soft-NUMA, si está disponible
2. Definir la afinidad del procesador
3. Crear grupos de recursos para los procesos externos, mediante [del regulador de recursos](../r/resource-governance-for-r-services.md)
4. Asignar el [grupos de cargas de trabajo](../../relational-databases/resource-governor/resource-governor-workload-group.md) a determinados grupos de afinidad

Para obtener más información, incluido el código de ejemplo, en este tutorial, consulte: [SQL optimización sugerencias y trucos (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**Otros recursos:**

+ [Soft-NUMA en SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    Cómo asignar nodos soft-NUMA a las CPU

## <a name="task-specific-optimizations"></a>Optimizaciones específicas de tareas

Esta sección resumen los métodos adoptados en estos casos prácticos y en otras pruebas para optimizar las cargas de trabajo de aprendizaje de máquina específica. Cargas de trabajo comunes incluyen entrenamiento del modelo, extracción de características y diseño de características y distintos escenarios de puntuación: lote de gran tamaño, lote pequeño y fila única.

### <a name="feature-engineering"></a>Ingeniería de características

Con R en una dificultad es que normalmente se procesa en una sola CPU. Se trata de un cuello de botella de rendimiento principales para muchas tareas, especialmente el diseño de características. En la solución de coincidencia de reanudación, la tarea de ingeniería ofrecida por sí sola crea 2.500 características de producto cruzado que tuvieron que se va a combinarse con las características de 100 originales. Esta tarea podría tardar una cantidad considerable de tiempo si todo lo que se ha realizado en una sola CPU.

Hay varias maneras de mejorar el rendimiento de ingeniería de características. Puede optimizar el código de R y mantener la extracción de características dentro del proceso de modelado o mover el proceso de ingeniería de características en SQL.

- Con R. Definir una función y, a continuación, páselo como argumento a [rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) durante el entrenamiento. Si el modelo admite el procesamiento en paralelo, la tarea de ingeniería de características puede procesarse mediante varias CPU. Con este enfoque, el equipo de ciencia de datos observa una mejora del rendimiento de 16% en términos de tiempo de puntuación. Sin embargo, este enfoque requiere un modelo que admite la ejecución en paralelo y una consulta que se puede ejecutar con un plan paralelo.

- Contexto de proceso de uso R con una instancia de SQL. En un entorno con varios procesadores con aislado recursos disponibles para la ejecución de lotes independientes, puede lograr una mayor eficacia mediante el aislamiento de las consultas SQL usadas para cada lote, para extraer datos de tablas y restringir los datos en el mismo grupo de cargas de trabajo. Los métodos utilizados para aislar los lotes incluyen la creación de particiones y uso de PowerShell para ejecutar consultas independientes en paralelo.

- Ejecución en paralelo ad hoc: En un contexto de proceso de SQL Server, que puede basarse en el motor de base de datos SQL para exigir la ejecución en paralelo si es posible y si se encuentra esa opción sea más eficaz.

- Usar Transact-SQL en un proceso independiente de características. Cálculo previo de los datos de características mediante SQL suele ser más rápido.

### <a name="prediction-scoring-in-parallel"></a>Predicción (puntuación) en paralelo

Una de las ventajas de SQL Server es su capacidad para controlar un gran número de filas en paralelo. En ningún sitio por lo que se marca esta ventaja al igual que en la puntuación. Por lo general el modelo no necesita acceso a todos los datos para puntuación, por lo que puede dividir los datos de entrada, con cada grupo de cargas de trabajo, una tarea de procesamiento.

También puede enviar los datos de entrada como una sola consulta y SQL Server, a continuación, analiza la consulta. Si un plan de consulta paralelo se puede crear para los datos de entrada, automáticamente crea particiones de datos asignados a los nodos y realiza requeridas combinaciones y agregaciones en paralelo también.

Si está interesado en los detalles de cómo definir un procedimiento almacenado para su uso para determinar la puntuación, vea el proyecto de ejemplo en [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR) y busque el archivo "step5_score_for_matching.sql". El ejemplo de script también inicio realiza un seguimiento de la consulta y horas de finalización y escribe la hora a la consola SQL para que se puede evaluar el rendimiento.

### <a name="concurrent-scoring-using-resource-groups"></a>Puntuación simultáneas mediante grupos de recursos

Para escalar verticalmente el problema de puntuación, una buena práctica es adoptar el enfoque de Map reduce en las que millones de elementos se dividen en varios lotes. A continuación, varios trabajos de puntuación se ejecutan simultáneamente. En este marco de trabajo son los lotes procesados en diferentes conjuntos de CPU, y los resultados se recopilan y volver a escribir en la base de datos.

Este es el enfoque usado en el escenario de coincidencia de reanudación; Sin embargo, la regulación de recursos en SQL Server es esencial para implementar este enfoque. Mediante la configuración de grupos de cargas de trabajo para trabajos de script externo, puede enrutar los trabajos de puntuación a grupos de procesadores diferentes de R y lograr un rendimiento más rápido.

Regulación de recursos también puede ayudar a asignar dividir los recursos disponibles en el servidor (CPU y memoria) para minimizar la competencia de la carga de trabajo. Puede configurar funciones clasificadoras para distinguir entre los distintos tipos de trabajos de R: por ejemplo, podría decidir que la puntuación llama desde una aplicación siempre tiene prioridad, mientras reentrenamiento trabajos tienen una prioridad baja. Este aislamiento de recursos podría mejorar el tiempo de ejecución y proporcionar un rendimiento más predecible.

### <a name="concurrent-scoring-using-powershell"></a>Puntuación simultáneas mediante PowerShell

Si decide dividir los datos usted mismo, puede usar scripts de PowerShell para ejecutar varias tareas simultáneas de puntuación. Para ello, use el cmdlet Invoke-SqlCmd e iniciar las tareas de puntuación en paralelo.

En el escenario de coincidencia de reanudación, la simultaneidad se diseñó como sigue:

- 20 procesadores se dividen en cuatro grupos de cinco CPUs. Cada grupo de CPU está ubicado en el mismo nodo NUMA.

- Número máximo de lotes simultáneos se estableció en ocho.

- Cada grupo de cargas de trabajo debe controlar dos tareas de puntuación. Tan pronto como una tarea ha finalizado la lectura de datos y puntuación se inicia, la otra tarea puede empezar a leer datos desde la base de datos.

Para ver los scripts de PowerShell para este escenario, abra el experiment.ps1 de archivo en el [proyecto Github](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips).

### <a name="storing-models-for-prediction"></a>Almacenar modelos de predicción

Cuando el entrenamiento y evaluación finaliza y se ha seleccionado un mejor modelo, se recomienda almacenar el modelo en la base de datos para que esté disponible para las predicciones. Cargar el modelo previamente calculado desde la base de datos para la predicción es eficaz, porque SQL Server machine learning usa algoritmos de serialización especial para almacenar y cargar los modelos cuando se mueven entre R y la base de datos.

> [!TIP]
> En SQL Server 2017, puede usar la función PREDICT para realizar la puntuación incluso si R no está instalado en el servidor. Se admiten tipos de modelos limitado, desde el paquete RevoScaleR.

Sin embargo, dependiendo del algoritmo que utilice, algunos modelos pueden ser bastante grandes, especialmente cuando se entrena con un gran conjunto de datos. Por ejemplo, los algoritmos como **lm** o **glm** generar muchos datos de resumen, junto con las reglas. Dado que hay límites en el tamaño de un modelo que se puede almacenar en una columna varbinary, recomendamos que eliminar artefactos innecesarios del modelo antes de almacenar el modelo en la base de datos de producción.

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Performance tuning para R - Introducción](../r/sql-server-r-services-performance-tuning.md)

[Optimización del rendimiento de R - configuración de SQL Server](../r/sql-server-configuration-r-services.md)

[Optimización del rendimiento de R: R optimización de código y los datos](../r/r-and-data-optimization-r-services.md)

[Los resultados del caso práctico: optimización del rendimiento](../r/performance-case-study-r-services.md)
