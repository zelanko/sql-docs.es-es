---
title: 'Rendimiento de SQL Server R Services: resultados y recursos'
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: aa56a9367271df2172236b133d85b5771089b1ac
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715043"
---
# <a name="performance-for-r-services-results-and-resources"></a>Rendimiento de R Services: resultados y recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artículo es el cuarto y el final de una serie que describe la optimización del rendimiento de R Services. En este artículo se resumen los métodos, los hallazgos y las conclusiones de dos casos prácticos que probaron varios métodos de optimización.

Los dos casos prácticos tenían objetivos diferentes:

+ El primer caso práctico, por parte del equipo de desarrollo de R Services, buscaba medir el impacto de las técnicas de optimización específicas
+ El segundo caso práctico, por parte de un equipo de científico de datos, experimentaba varios métodos para determinar las mejores optimizaciones para un escenario específico de puntuación de gran volumen.

En este tema se enumeran los resultados detallados del primer caso práctico. En el segundo caso práctico, un resumen describe las conclusiones generales. Al final de este tema se incluyen vínculos a todos los scripts y datos de ejemplo, así como a los recursos utilizados por los autores originales.

## <a name="performance-case-study-airline-dataset"></a>Caso práctico de rendimiento: Conjunto de una línea aérea

Este caso práctico del equipo de desarrollo de SQL Server R Services probó los efectos de varias optimizaciones. Se ha creado un único modelo rxLogit y se ha realizado la puntuación en el conjunto de datos de la línea aérea. Las optimizaciones se aplicaron durante los procesos de entrenamiento y puntuación para evaluar los impactos individuales.

- GitHub: [Datos de ejemplo y scripts](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para el estudio de SQL Server optimizaciones

### <a name="test-methods"></a>Métodos de prueba

1. El conjunto de filas de línea aérea consta de una sola tabla de 10 millones de filas. Se descargó y cargó de forma masiva en SQL Server.
2. Se realizaron seis copias de la tabla.
3. Se aplicaron varias modificaciones a las copias de la tabla para probar SQL Server características como la compresión de página, la compresión de filas, la indexación, el almacén de datos en columnas, etc.
4. El rendimiento se midió antes y después de aplicar cada optimización.

| Nombre de tabla| Descripción|
|------|------|
| *airline* | Datos convertidos desde el archivo xdf original con `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido en entero en lugar de en cadena. También se agrega una columna *rowNum*.|
| *airlineWithIndex*    | Los mismos datos que la tabla *airlineWithIntCol*, pero con un único índice agrupado por medio de la columna *rowNum*.|
| *airlineWithPageComp* | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de página habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineWithRowComp*  | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de fila habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineColumnar*     | Almacén de columnas con un único índice agrupado. Esta tabla se rellena con datos de un archivo csv limpio.|

Cada prueba consta de estos pasos:

1. Antes de cada prueba, se indujo a la recolección de elementos no utilizados de R.
2. Se creó un modelo de regresión logística basado en los datos de la tabla. El valor de *rowsPerRead* en cada prueba estaba establecido en 500 000.
3. Las puntuaciones se generaron con el modelo entrenado
4. Cada prueba se ejecutó seis veces. La hora de la primera ejecución (la "ejecución en frío") se ha quitado. Para permitir el valor atípico ocasional, el tiempo **máximo** entre las cinco ejecuciones restantes también se ha quitado. La media de las cuatro ejecuciones restantes se usó para calcular la media de tiempo de ejecución transcurrido de cada prueba.
5. Las pruebas se ejecutaron con el parámetro *reportProgress* con el valor 3 (= intervalos y progreso de los informes). Cada archivo de salida contiene información sobre el tiempo invertido en e/s, el tiempo de transición y el tiempo de proceso. Estos valores de tiempo son útiles a la hora de solucionar problemas y realizar diagnósticos.
6. La salida de la consola también se dirigió a un archivo en el directorio de salida.
7. Los scripts de prueba procesaron las horas en estos archivos para calcular el tiempo medio de las ejecuciones.

Por ejemplo, los siguientes resultados son las horas de una sola prueba. Los principales intervalos de interés son **Total read time** (tiempo de E/S) y **Transition time** (sobrecarga al configurar procesos de cálculo).

**Intervalos de muestra**

```text
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

Se recomienda que descargue y modifique los scripts de prueba para ayudarle a solucionar problemas con R Services o con las funciones de RevoScaleR.

### <a name="test-results-all"></a>Resultados de pruebas (todos)

En esta sección se comparan los resultados de antes y después de cada una de las pruebas.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamaño de los datos con compresión y un almacén de tablas en columnas

En la primera prueba se comparaba el uso de la compresión y una tabla en columnas para reducir el tamaño de los datos.

| Nombre de tabla            | Filas     | Reservado   | Datos       | index_size | No utilizado  | % Saving (reserved) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10 000 000 | 2 978 816 KB | 2 972 160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10 000 000 | 625 784 KB  | 623 744 KB  | 1352 KB    | 688 KB  | 79 %                 |
| *airlineWithRowComp*  | 10 000 000 | 1 262 520 KB | 1 258 880 KB | 2552 KB    | 1088 KB | 58 %                 |
| *airlineColumnar*     | 9 999 999  | 201 992 KB  | 201 624 KB  | N/D        | 368 KB  | 93 %                 |

**Sacar**

La mayor reducción del tamaño de los datos se logra mediante la aplicación de un índice de almacén de columnas, seguido de la compresión de página.

#### <a name="effects-of-compression"></a>Efectos de la compresión

En esta prueba se comparan las ventajas de la compresión de filas, la compresión de página y ninguna compresión. Un modelo se ha entrenado `rxLinMod` con datos de tres tablas de datos diferentes. Se usó la misma fórmula y la misma consulta en todas las tablas.

| Nombre de tabla            | Nombre de la prueba       | numTasks | Promedio de tiempo |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5,6775       |
|                       | NoCompression-Parallel| 4        | 5,1775       |
| *airlineWithPageComp* | NoCompression | 1        | 6,7875       |
|                       | PageCompression: paralelo | 4        | 5,3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6,1325       |
|                       | RowCompression: paralelo  | 4        | 5,2375       |

**Sacar**

La compresión por sí sola no parece servir de ayuda. En este ejemplo, el aumento de la CPU para controlar la compresión compensa la disminución del tiempo de e/s.

Con todo, cuando la prueba se ejecuta en paralelo estableciendo *numTasks* en 4, el promedio de tiempo disminuye.

En los conjuntos de datos grandes, es posible que el efecto de la compresión sea más evidente. La compresión depende del conjunto de datos y de los valores, por lo que puede que sea necesario experimentar para averiguar el efecto que la compresión tiene en el conjunto de datos.

### <a name="effect-of-windows-power-plan-options"></a>Efecto de las opciones del plan de energía de Windows

En este experimento, `rxLinMod` se usó con la tabla *airlineWithIntCol*. El plan de energía de Windows se estableció en equilibrado o **alto rendimiento**. En todas las pruebas, *numTasks* se estableció en 1. La prueba se ejecutó seis veces y se realizó dos veces en ambas opciones de energía para investigar la variabilidad de los resultados.

Opción de potencia de **alto rendimiento** :

| Nombre de la prueba | Ejecute \#: | Tiempo transcurrido | Promedio de tiempo |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,57 segundos |              |
|           | 2      | 3,45 segundos |              |
|           | 3      | 3,45 segundos |              |
|           | 4      | 3,55 segundos |              |
|           | 5      | 3,55 segundos |              |
|           | 6      | 3,45 segundos |              |
|           |        |              | 3,475        |
|           | 1      | 3,45 segundos |              |
|           | 2      | 3,53 segundos |              |
|           | 3      | 3,63 segundos |              |
|           | 4      | 3,49 segundos |              |
|           | 5      | 3,54 segundos |              |
|           | 6      | 3,47 segundos |              |
|           |        |              | 3,5075       |

Opción de energía **Equilibrado**:

| Nombre de la prueba | Ejecute \#: | Tiempo transcurrido | Promedio de tiempo |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3,89 segundos |              |
|           | 2      | 4,15 segundos |              |
|           | 3      | 3,77 segundos |              |
|           | 4      | 5 segundos    |              |
|           | 5      | 3,92 segundos |              |
|           | 6      | 3,8 segundos  |              |
|           |        |              | 3,91         |
|           | 1      | 3,82 segundos |              |
|           | 2      | 3,84 segundos |              |
|           | 3      | 3,86 segundos |              |
|           | 4      | 4,07 segundos |              |
|           | 5      | 4,86 segundos |              |
|           | 6      | 3,75 segundos |              |
|           |        |              | 3,88         |

**Sacar**

El tiempo de ejecución es más coherente y más rápido cuando se usa el plan de energía de **alto rendimiento** de Windows.

#### <a name="using-integer-vs-strings-in-formulas"></a>Usar cadenas de tipo entero frente a cadenas en fórmulas

Esta prueba evaluó el impacto de la modificación del código R para evitar un problema común con factores de cadena. En concreto, se ha entrenado un `rxLinMod` modelo mediante el uso de dos tablas: en el primero, los factores se almacenan como cadenas; en la segunda tabla, los factores se almacenan como enteros.

+ En la tabla de *líneas aéreas* , la columna [DayOfWeek] contiene cadenas. El parámetro _colInfo_ se usó para especificar los niveles de factor (lunes, martes,...)

+  En el caso de la tabla *airlineWithIndex* , [DayOfWeek] es un entero. No se especificó el parámetro _colInfo_ .

+ En ambos casos, se usó la misma fórmula: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nombre de tabla          | Nombre de la prueba   | Promedio de tiempo |
|---------------------|-------------|--------------|
| *Vuelta*           | *FactorCol* | 10,72        |
| *airlineWithIntCol* | *IntCol*    | 3,4475       |

**Sacar**

El uso de enteros en lugar de cadenas para factores no supone una ventaja clara.

### <a name="avoiding-transformation-functions"></a>Evitar las funciones de transformación

En esta prueba, se ha entrenado un modelo `rxLinMod`mediante, pero se ha cambiado el código entre las dos ejecuciones:

+ En la primera ejecución, se aplicó una función de transformación como parte de la creación del modelo. 
+ En la segunda ejecución, los valores de las características se han calculado previamente y están disponibles, por lo que no se requiere ninguna función de transformación.

| Nombre de la prueba             | Promedio de tiempo |
|-----------------------|--------------|
| WithTransformation    | 5,1675       |
| WithoutTransformation | 4,7          |

**Sacar**

El tiempo de entrenamiento era más corto cuando **no** se usa una función de transformación. En otras palabras, el modelo se entrenó más rápidamente al usar columnas que se han calculado previamente y se han guardado en la tabla.

Se espera que el ahorro sea mayor si hay muchas transformaciones más y el conjunto de datos era mayor (\> 100M).

### <a name="using-columnar-store"></a>Usar el almacén de columnas

Esta prueba evaluó las ventajas de rendimiento que supone el uso de un almacén de datos y un índice de columnas. El mismo modelo se ha entrenado `rxLinMod` con y sin transformaciones de datos.

+ En la primera ejecución, la tabla de datos usaba un almacén de filas estándar.
+ En la segunda ejecución, se usó un almacén de columnas.

| Nombre de tabla         | Nombre de la prueba | Promedio de tiempo |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4,67         |
| *airlineColumnar*  | ColStore  | 4,555        |

**Sacar**

El rendimiento es mejor con el almacén de columnas que con el almacén de filas estándar. Se puede esperar una diferencia significativa en el rendimiento en conjuntos de datos\> más grandes (100 M).

### <a name="effect-of-using-the-cube-parameter"></a>Efecto de usar el parámetro Cube

La finalidad de esta prueba era determinar si la opción de RevoScaleR para usar el parámetro de **cubo** precalculado puede mejorar el rendimiento. Un modelo se entrenó mediante `rxLinMod`usando esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

En la tabla, los factores *DayOfWeek* se almacenan como una cadena.

| Nombre de la prueba     | Parámetro Cube | numTasks | Promedio de tiempo | Predicción de fila única (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91,0725      | 9,959204                        |
|               |                | 4        | 44,09        | 9,959204                        |
|               | `cube = T`     | 1        | 21,1125      | 9,959204                        |
|               |                | 4        | 8,08         | 9,959204                        |

**Sacar**

El uso del argumento de parámetro Cube mejora claramente el rendimiento.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efecto de cambiar maxDepth para los modelos rxDTree

En este experimento, el `rxDTree` algoritmo se usó para crear un modelo en la tabla *airlineColumnar* . En esta prueba *numTasks* se estableció en 4. Se usaron varios valores diferentes para *maxDepth* para demostrar cómo afecta la profundidad del árbol al tiempo de ejecución.

| Nombre de la prueba       | maxDepth | Promedio de tiempo |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10,1975      |
|                 | 2        | 13,2575      |
|                 | 4        | 19,27        |
|                 | 8        | 45,5775      |
|                 | 16       | 339,54       |

**Sacar**

A medida que aumenta la profundidad del árbol, aumenta exponencialmente el número total de nodos. El tiempo transcurrido para crear el modelo también aumentó significativamente.

### <a name="prediction-on-a-stored-model"></a>Predicción en un modelo almacenado

La finalidad de esta prueba era determinar el impacto en el rendimiento de la puntuación cuando el modelo entrenado se guarda en una tabla de SQL Server en lugar de generarse como parte del código que se está ejecutando actualmente. Para puntuar, el modelo almacenado se carga desde la base de datos y las predicciones se crean mediante una trama de datos de una fila en la memoria (contexto de proceso local).

Los resultados de la prueba muestran el tiempo necesario para guardar el modelo y el tiempo que se tarda en cargar el modelo y predecir.

| Nombre de tabla | Nombre de la prueba | Promedio de tiempo (en entrenar el modelo) | Tiempo en guardar/cargar el modelo|
|------------|------------|------------|------------|
| airline    | SaveModel| 21,59| 2,08|
| airline    | LoadModelAndPredict | | 2,09 (tiempo de la predicción incluido) |

**Sacar**

Cargar un modelo entrenado a partir de una tabla es claramente una manera más rápida de realizar la predicción. Se recomienda evitar crear el modelo y realizar la puntuación en el mismo script.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Caso práctico: Optimización de la tarea para reanudar la búsqueda de coincidencias

El modelo resume-matching fue desarrollado por Microsoft Data científico ke Huang para probar el rendimiento del código R en SQL Server y, al hacerlo, ayuda a los científicos de datos a crear soluciones escalables y empresariales.

### <a name="methods"></a>Métodos

Los paquetes RevoScaleR y MicrosoftML se usaron para entrenar un modelo predictivo en una solución de R compleja que implica grandes conjuntos de valores. Las consultas SQL y el código R eran idénticos en todas las pruebas. Las pruebas se realizaron en una sola máquina virtual de Azure con SQL Server instalado. Después, el autor compararía la puntuación con y sin las siguientes optimizaciones proporcionadas por SQL Server:

- Tablas en memoria
- Soft-NUMA
- regulador de recursos

Para evaluar el efecto de Soft-NUMA en la ejecución del script de R, el equipo de ciencia de datos probó la solución en una máquina virtual de Azure con 20 núcleos físicos. En estos núcleos físicos, se crearon automáticamente cuatro nodos NUMA de software, de modo que cada nodo contenía cinco núcleos.

La CPU affinitization se aplicó en el escenario de búsqueda de coincidencias, para evaluar el impacto en los trabajos de R. Se crearon cuatro **grupos de recursos de SQL** y cuatro grupos de **recursos externos** , y se especificó la afinidad de CPU para asegurarse de que se utilizaría el mismo conjunto de CPU en cada nodo.

Cada uno de los grupos de recursos se asignó a un grupo de cargas de trabajo diferente para optimizar el uso del hardware. La razón es que soft-NUMA y la afinidad de la CPU no pueden dividir la memoria física en los nodos NUMA físicos. por lo tanto, por definición, todos los nodos NUMA de software que se basan en el mismo nodo físico NUMA deben usar memoria en el mismo bloque de memoria del sistema operativo. En otras palabras, no hay afinidad entre la memoria y el procesador.

Se usó el siguiente proceso para crear esta configuración:

1. Reduzca la cantidad de memoria asignada de forma predeterminada a SQL Server.

2. Cree cuatro grupos nuevos para ejecutar los trabajos de R en paralelo.

3. Cree cuatro grupos de cargas de trabajo de modo que cada grupo de cargas de trabajo esté asociado a un grupo de recursos.

4. Reinicie Resource Governor con los nuevos grupos de cargas de trabajo y las asignaciones.

5. Cree una función clasificadora definida por el usuario (UDF) para asignar distintas tareas en grupos de cargas de trabajo diferentes.

6. Actualice la configuración de Resource Governor para usar la función para los grupos de cargas de trabajo adecuados.

### <a name="results"></a>Resultados

La configuración que tenía el mejor rendimiento en el estudio de la búsqueda de coincidencias es la siguiente:

-   Cuatro grupos de recursos internos (por SQL Server)

-   Cuatro grupos de recursos externos (para trabajos de script externo)

-   Cada grupo de recursos está asociado a un grupo de cargas de trabajo específico

-   Cada grupo de recursos se asigna a diferentes CPU

-   Uso máximo de memoria interna (por SQL Server) = 30%

-   Memoria máxima para el uso de las sesiones de R = 70%

Para el modelo de búsqueda de coincidencias, el uso de scripts externos era pesado y no había otros servicios de motor de base de datos en ejecución. Por lo tanto, los recursos asignados a los scripts externos se aumentaron al 70%, lo que demostró la mejor configuración para el rendimiento del script.

Esta configuración se llegó a experimentando con valores diferentes. Si utiliza un hardware diferente o una solución diferente, la configuración óptima podría ser diferente. Experimente siempre para encontrar la mejor configuración para su caso.

En la solución optimizada, se puntuaron 1,1 millones filas de datos (con características 100) en menos de 8,5 segundos en un equipo de 20 núcleos. Las optimizaciones mejoraron considerablemente el rendimiento en términos de tiempo de puntuación.

Los resultados también sugieren que el **número de características** tenía un impacto significativo en el tiempo de puntuación. La mejora era aún más destacada cuando se usaban más características en el modelo de predicción.

Le recomendamos que lea este artículo del blog y el tutorial que lo acompaña para obtener una explicación detallada.

-   [Sugerencias y trucos para la optimización de machine learning en SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muchos usuarios han observado que hay una pequeña pausa, ya que el tiempo de ejecución de R (o Python) se carga por primera vez. Por esta razón, como se describe en estas pruebas, la hora de la primera ejecución se mide a menudo, pero después se descarta. El almacenamiento en caché subsiguiente podría producir diferencias de rendimiento significativas entre la primera y la segunda ejecución. También hay cierta sobrecarga cuando los datos se mueven entre SQL Server y el tiempo de ejecución externo, especialmente si los datos se pasan a través de la red en lugar de cargarse directamente desde SQL Server.

Por todas estas razones, no hay ninguna solución única para mitigar este tiempo de carga inicial, ya que el impacto en el rendimiento varía significativamente en función de la tarea. Por ejemplo, el almacenamiento en caché se realiza para la puntuación de fila única en lotes. por lo tanto, las operaciones de puntuación sucesivas son mucho más rápidas y ni el modelo ni el Runtime de R se recargan. También puede usar la [puntuación nativa](../sql-native-scoring.md) para evitar cargar el tiempo de ejecución de R por completo.

Para entrenar modelos grandes o puntuaciones en lotes grandes, la sobrecarga puede ser mínima en comparación con las ventajas de evitar el movimiento de datos o el procesamiento paralelo y el streaming. Vea esta entrada de blog para obtener más información sobre el rendimiento:

+ [Uso de R para detectar fraudes en 1 millón transacciones por segundo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

A continuación se incluyen vínculos a información, herramientas y scripts que se usan en el desarrollo de estas pruebas.

+ Scripts de prueba de rendimiento y vínculos a los datos: [Datos de ejemplo y scripts para el estudio de SQL Server optimizaciones](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artículo que describe la solución de búsqueda de coincidencias: [Sugerencias y trucos de optimización para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados en la optimización de SQL para la solución de búsqueda de coincidencias: [Repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Más información acerca de la administración de Windows Server

+ [Determinar el tamaño apropiado del archivo de paginación para las versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880)

+ [Descripción de NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Cómo SQL Server admite NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [NUMA de software](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Más información sobre las optimizaciones de SQL Server

+ [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introducción a las tablas con optimización para memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demostración: Mejora del rendimiento de OLTP en memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Deshabilitar compresión de una tabla o un índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Más información sobre la administración de SQL Server

+ [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

+ [Presentación de Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [Regulación de recursos para R Services](resource-governance-for-r-services.md)

+ [Cómo crear un grupo de recursos para R](how-to-create-a-resource-pool-for-r.md)

+ [Un ejemplo de configuración de Resource Governor](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Herramientas

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd) (Herramienta DISKSPD de generador de carga de almacenamiento/prueba de rendimiento)

+ [Referencia de la utilidad FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Otros artículos de esta serie

[Optimización del rendimiento para R: introducción](sql-server-r-services-performance-tuning.md)

[Ajuste del rendimiento para la configuración de R-SQL Server](sql-server-configuration-r-services.md)

[Optimización del rendimiento de código R-R y optimización de datos](r-and-data-optimization-r-services.md)

[Optimización del rendimiento: resultados de los casos prácticos](performance-case-study-r-services.md)
