---
title: 'Rendimiento de SQL Server R Services: resultados y los recursos: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 392a6da09827355e6bc9a901b0e4580e5eb72bf5
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645557"
---
# <a name="performance-for-r-services-results-and-resources"></a>Rendimiento de R Services: los resultados y los recursos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo es el cuarto y final de una serie que describe la optimización del rendimiento para R Services. En este artículo se resume los métodos, las conclusiones y las conclusiones de dos casos prácticos que probar distintos métodos de optimización.

Los dos casos prácticos tenía objetivos distintos:

+ El primer caso práctico, por el equipo de desarrollo de R Services, busca medir el impacto de técnicas de optimización específicas
+ El segundo caso práctico, por un equipo de científicos de datos experimentó con varios métodos para determinar las mejores optimizaciones para un escenario concreto de puntuación de gran volumen.

En este tema se enumera los resultados detallados del primer caso práctico. Para el segundo caso práctico, un resumen describe las conclusiones generales. Al final de este tema son vínculos a todos los recursos utilizados por los autores originales y datos de ejemplo y scripts.

## <a name="performance-case-study-airline-dataset"></a>Caso práctico de rendimiento: Conjunto de datos Airline

En este caso práctico por el equipo de desarrollo de SQL Server R Services probar los efectos de varias optimizaciones. Se creó un modelo único rxLogit y puntuación realizadas en el conjunto de datos de la compañía aérea. Las optimizaciones se aplicaron durante el entrenamiento y puntuación de procesos para valorar impactos individuales.

- Github: [Los scripts y datos de ejemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) de estudio de las optimizaciones de SQL Server

### <a name="test-methods"></a>Métodos de prueba

1. El conjunto de datos Airline consiste en una única tabla de 10 millones de filas. Se ha descargado y la carga masiva en SQL Server.
2. Se realizaron seis copias de la tabla.
3. Varias modificaciones se aplicaron a las copias de la tabla para probar las características de SQL Server como la compresión de página, la compresión row, indización, el almacén de datos en columnas, etcetera.
4. Se midió el rendimiento antes y después de que se aplicó la optimización de cada.

| Nombre de la tabla| Descripción|
|------|------|
| *airline* | Datos convertidos desde el archivo xdf original con `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido en entero en lugar de en cadena. También se agrega una columna *rowNum*.|
| *airlineWithIndex*    | Los mismos datos que la tabla *airlineWithIntCol*, pero con un único índice agrupado por medio de la columna *rowNum*.|
| *airlineWithPageComp* | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de página habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineWithRowComp*  | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de fila habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineColumnar*     | Almacén de columnas con un único índice agrupado. Esta tabla se rellena con datos de un archivo csv limpio.|

Cada prueba estaba formada por estos pasos:

1. Antes de cada prueba, se indujo a la recolección de elementos no utilizados de R.
2. Un modelo de regresión logística se creó basado en la tabla de datos. El valor de *rowsPerRead* en cada prueba estaba establecido en 500 000.
3. Las puntuaciones se generaron mediante el modelo entrenado
4. Cada prueba se ejecutó seis veces. Se eliminó el tiempo de la primera ejecución (la "ejecución en frío"). Para permitir que el valor atípico ocasional, el **máximo** también se eliminó el tiempo entre las cinco ejecuciones restantes. La media de las cuatro ejecuciones restantes se usó para calcular la media de tiempo de ejecución transcurrido de cada prueba.
5. Las pruebas se ejecutaron mediante el *reportProgress* parámetro con el valor 3 (= los intervalos de informes y el progreso). Cada archivo de salida contiene información sobre el tiempo invertido en E/S, tiempo de transición y tiempo de proceso. Estos valores de tiempo son útiles a la hora de solucionar problemas y realizar diagnósticos.
6. La salida de la consola también se dirige a un archivo en el directorio de salida.
7. Los scripts de prueba procesan las horas en estos archivos para calcular el promedio de tiempo a través de ejecuciones.

Por ejemplo, los resultados siguientes son las horas de una única prueba. Los principales intervalos de interés son **Total read time** (tiempo de E/S) y **Transition time** (sobrecarga al configurar procesos de cálculo).

**Intervalos de ejemplo**

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

Se recomienda que descargue y modifique los scripts de prueba para ayudarle a solucionar problemas con R Services o con funciones de RevoScaleR.

### <a name="test-results-all"></a>Probar los resultados (todos)

Esta sección se comparan antes y después los resultados para cada una de las pruebas.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamaño de los datos con la compresión y un almacén de columnas de tabla

La primera prueba compara el uso de la compresión y una tabla en columnas para reducir el tamaño de los datos.

| Nombre de la tabla            | Filas     | Reservado   | Datos       | index_size | No utilizado  | % Saving (reserved) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10 000 000 | 2 978 816 KB | 2 972 160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10 000 000 | 625 784 KB  | 623 744 KB  | 1352 KB    | 688 KB  | 79 %                 |
| *airlineWithRowComp*  | 10 000 000 | 1 262 520 KB | 1 258 880 KB | 2552 KB    | 1088 KB | 58 %                 |
| *airlineColumnar*     | 9 999 999  | 201 992 KB  | 201 624 KB  | n/d        | 368 KB  | 93 %                 |

**Conclusiones**

La mayor reducción de tamaño de los datos se logra aplicando un índice de almacén de columnas, seguido de compresión de página.

#### <a name="effects-of-compression"></a>Efectos de la compresión

Esta prueba compara las ventajas de la compresión de fila, compresión de página y no hay compresión. Un modelo se entrenó con `rxLinMod` en los datos de tres tablas de datos diferentes. Se usó la misma fórmula y la misma consulta en todas las tablas.

| Nombre de la tabla            | Nombre de la prueba       | numTasks | Promedio de tiempo |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5,6775       |
|                       | NoCompression - paralelo| 4        | 5,1775       |
| *airlineWithPageComp* | NoCompression | 1        | 6,7875       |
|                       | PageCompression - paralelo | 4        | 5,3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6,1325       |
|                       | RowCompression - paralelo  | 4        | 5,2375       |

**Conclusiones**

La compresión a secas no parece ayudar. En este ejemplo, el aumento de la CPU para controlar la compresión compensa la disminución del tiempo de E/S.

Con todo, cuando la prueba se ejecuta en paralelo estableciendo *numTasks* en 4, el promedio de tiempo disminuye.

En los conjuntos de datos grandes, es posible que el efecto de la compresión sea más evidente. La compresión depende del conjunto de datos y de los valores, por lo que puede que sea necesario experimentar para averiguar el efecto que la compresión tiene en el conjunto de datos.

### <a name="effect-of-windows-power-plan-options"></a>Efecto de las opciones de plan de energía de Windows

En este experimento, `rxLinMod` se usó con la tabla *airlineWithIntCol*. El Plan de energía de Windows se ha establecido en **equilibrado** o **de alto rendimiento**. En todas las pruebas, *numTasks* se estableció en 1. La prueba se ejecutó seis veces y se realiza dos veces en ambas opciones de energía para investigar la variabilidad de los resultados.

**Alto rendimiento** opción de energía:

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

**Conclusiones**

El tiempo de ejecución es más coherente y más rápido cuando se usa el Windows **de alto rendimiento** plan de energía.

#### <a name="using-integer-vs-strings-in-formulas"></a>Uso de entero frente a las cadenas en fórmulas

Esta prueba evalúa el impacto de la modificación del código de R para evitar un problema común con factores de cadena. En concreto, un modelo se entrenó con `rxLinMod` con dos tablas: la primera, factores se almacenan como cadenas; la segunda tabla, factores se almacenan como enteros.

+ Para el *airline* tabla, la columna [DayOfWeek] contiene cadenas. El _colInfo_ parámetro se usa para especificar los niveles de factor (lunes, el martes,...)

+  Para el *airlineWithIndex* tabla, [DayOfWeek] es un entero. El _colInfo_ no se especificó el parámetro.

+ En ambos casos, se usó la misma fórmula: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nombre de la tabla          | Nombre de la prueba   | Promedio de tiempo |
|---------------------|-------------|--------------|
| *Compañía aérea*           | *FactorCol* | 10,72        |
| *airlineWithIntCol* | *IntCol*    | 3,4475       |

**Conclusiones**

Hay una ventaja evidente al usar enteros en lugar de cadenas de factores.

### <a name="avoiding-transformation-functions"></a>Evitar funciones de transformación

En esta prueba, se entrena un modelo con `rxLinMod`, pero se cambió el código entre las dos ejecuciones:

+ En la primera ejecución, se aplica una función de transformación como parte de la creación del modelo. 
+ En la segunda ejecución, los valores de las características eran precalculadas y está disponible, por lo que no se necesitaba ninguna función de transformación.

| Nombre de la prueba             | Promedio de tiempo |
|-----------------------|--------------|
| WithTransformation    | 5,1675       |
| WithoutTransformation | 4,7          |

**Conclusiones**

Tiempo de entrenamiento fue más corto cuando **no** mediante una función de transformación. En otras palabras, el modelo se entrenó con mayor rapidez cuando se usan columnas que se han calculado previamente y que se conservan en la tabla.

El ahorro se espera que sea mayor si se han producido muchas más transformaciones y el conjunto de datos eran más grandes (\> 100 M).

### <a name="using-columnar-store"></a>Uso de almacén de columnas

Esta prueba evalúa las ventajas de rendimiento de usar un almacén de datos en columnas y un índice. El mismo modelo se entrenó con `rxLinMod` y ninguna transformación de datos.

+ En la primera ejecución, la tabla de datos utiliza un almacén de filas estándar.
+ En la segunda ejecución, se usó un almacén de columnas.

| Nombre de la tabla         | Nombre de la prueba | Promedio de tiempo |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4,67         |
| *airlineColumnar*  | ColStore  | 4,555        |

**Conclusiones**

Rendimiento es mejor con el almacén de columnas que con el almacén de filas estándar. Una diferencia significativa en el rendimiento se puede esperar en grandes conjuntos de datos (\> 100 M).

### <a name="effect-of-using-the-cube-parameter"></a>Efecto de usar el parámetro de cubo

El objetivo de esta prueba era determinar si la opción de RevoScaleR para usar el precalculadas **cubo** parámetro puede mejorar el rendimiento. Un modelo se entrenó con `rxLinMod`, utilizando esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

En la tabla, los factores *DayOfWeek* se almacena como una cadena.

| Nombre de la prueba     | Parámetro Cube | numTasks | Promedio de tiempo | Única fila (arrdelay_pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91,0725      | 9,959204                        |
|               |                | 4        | 44,09        | 9,959204                        |
|               | `cube = T`     | 1        | 21,1125      | 9,959204                        |
|               |                | 4        | 8,08         | 9,959204                        |

**Conclusiones**

El uso del argumento del parámetro de cubo claramente mejora el rendimiento.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efecto del cambio maxDepth para los modelos rxDTree

En este experimento, el `rxDTree` algoritmo se usó para crear un modelo en el *airlineColumnar* tabla. En esta prueba *numTasks* se estableció en 4. Varios valores diferentes para *maxDepth* se usaron para demostrar cómo modificar la profundidad del árbol afecta al tiempo de ejecución.

| Nombre de la prueba       | maxDepth | Promedio de tiempo |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10,1975      |
|                 | 2        | 13,2575      |
|                 | 4        | 19,27        |
|                 | 8        | 45,5775      |
|                 | 16       | 339,54       |

**Conclusiones**

A medida que aumenta la profundidad del árbol, el número total de nodos aumenta exponencialmente. El tiempo transcurrido para crear el modelo también aumenta significativamente.

### <a name="prediction-on-a-stored-model"></a>Predicción en un modelo almacenado

El objetivo de esta prueba era determinar el impacto de rendimiento en la puntuación cuando el modelo entrenado se guarda en una tabla de SQL Server en lugar de generados como parte del código en ejecución actualmente. Para puntuar, el modelo almacenado se carga desde la base de datos y las predicciones se crean mediante una trama de datos de una fila en la memoria (contexto de cálculo local).

Los resultados de pruebas muestran el tiempo para guardar el modelo y el tiempo necesario para cargar el modelo y predicción.

| Nombre de la tabla | Nombre de la prueba | Promedio de tiempo (en entrenar el modelo) | Tiempo en guardar/cargar el modelo|
|------------|------------|------------|------------|
| airline    | SaveModel| 21,59| 2,08|
| airline    | LoadModelAndPredict | | 2,09 (tiempo de la predicción incluido) |

**Conclusiones**

Al cargar un modelo entrenado de una tabla es claramente una manera más rápida para hacer la predicción. Se recomienda que evite crear un modelo y realizar todo en el mismo script de puntuación.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Caso práctico: Optimización de la tarea de coincidencia de reanudación

El modelo de coincidencia de reanudación fue desarrollado por científicos de datos de Microsoft Ke Huang para probar el rendimiento del código de R en SQL Server y realizando en ese datos de ayuda creación escalables, los científicos de soluciones de nivel empresarial.

### <a name="methods"></a>Métodos

Los paquetes RevoScaleR y de MicrosoftML se usaron para entrenar un modelo predictivo en una solución de R complejo que implican grandes conjuntos de datos. Consultas SQL y el código de R fueran idénticos en todas las pruebas. Las pruebas se realizaron en una sola máquina virtual de Azure con SQL Server instalado. El autor, a continuación, en comparación con los tiempos de puntuación con y sin las siguientes optimizaciones de SQL Server:

- Tablas en memoria
- Soft-NUMA
- regulador de recursos

Para evaluar el efecto de soft-NUMA en ejecución de scripts de R, el equipo de ciencia de datos probado la solución en una máquina virtual de Azure con 20 núcleos físicos. En estos núcleos físicos, cuatro nodos soft-NUMA se crearon automáticamente, tal que cada nodo contiene cinco núcleos.

Se aplicó afinamiento de CPU en el escenario de coincidencia de reanudación, para evaluar el impacto en los trabajos de R. Cuatro **grupos de recursos SQL** y cuatro **grupos de recursos externos** fueron creadas, y no se especificó la afinidad de CPU para asegurarse de que se usaría el mismo conjunto de CPU en cada nodo.

Cada uno de los grupos de recursos se asignó a un grupo de cargas de trabajo diferente, para optimizar la utilización del hardware. El motivo es que Soft-NUMA y afinidad de CPU no puede dividir la memoria física en los nodos NUMA físicos; por lo tanto, por definición, todos los nodos NUMA temporales que se basan en el mismo nodo NUMA físico deben usar memoria en el mismo bloque de memoria del sistema operativo. En otras palabras, no hay ninguna afinidad de procesador de memoria.

El siguiente proceso se usó para crear esta configuración:

1. Reducir la cantidad de memoria asignada de forma predeterminada en SQL Server.

2. Cree cuatro grupos nuevos para ejecutar los trabajos de R en paralelo.

3. Crear cuatro grupos de cargas de trabajo de forma que cada grupo de cargas de trabajo está asociado a un grupo de recursos.

4. Reinicie el regulador de recursos con los nuevos grupos de cargas de trabajo y las asignaciones.

5. Crear una función clasificadora definida por el usuario (UDF) para asignar diferentes tareas en grupos de cargas de trabajo diferente.

6. Actualice la configuración del regulador de recursos para usar la función para los grupos de cargas de trabajo adecuado.

### <a name="results"></a>Resultado

La configuración que tenía el mejor rendimiento en la coincidencia de reanudación de estudio fue el siguiente:

-   Cuatro grupos de recursos internos (para SQL Server)

-   Cuatro grupos de recursos externos (para los trabajos de script externo)

-   Cada grupo de recursos está asociado a un grupo de cargas de trabajo concreto

-   Se asigna cada grupo de recursos para diferentes CPU

-   Uso máximo de memoria interna (para SQL Server) = 30%

-   Cantidad máxima de memoria para su uso en las sesiones de R = 70%

Para el modelo de coincidencia de reanudar el uso de scripts externos estaba pesado y no había ninguna base de datos de otro servicios de motor de ejecución. Por lo tanto, los recursos asignados a los scripts externos se han aumentado al 70%, lo que resultó ser la mejor configuración para el rendimiento de la secuencia de comandos.

Esta configuración se ha llegado al experimentar con diferentes valores. Si usas un hardware diferente o una solución diferente, la configuración óptima puede ser diferente. Siempre experimentar para encontrar la mejor configuración para su caso.

En la solución optimizada, se puntúan 1.1 millón de filas de datos (con 100 características) en menos de 8,5 segundos en un equipo de 20 núcleos. Las optimizaciones mejoraron considerablemente el rendimiento en términos de tiempo de puntuación.

Los resultados también sugieren que el **número de características** tenía un impacto significativo en el momento de puntuación. La mejora era incluso más destacada más características que se usaron en el modelo de predicción.

Se recomienda que lea este artículo de blog y el tutorial que lo acompaña para obtener información detallada.

-   [Optimización sugerencias y trucos para el aprendizaje automático en SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muchos usuarios han indican que hay una pausa pequeña como el tiempo de ejecución de R (o Python) se carga por primera vez. Por este motivo, como se describe en estas pruebas, la hora de la primera ejecución se suele medirse pero más adelante se descartan. Posterior almacenamiento en caché puede dar lugar a diferencias de rendimiento notable entre el primer y segundo se ejecuta. También hay cierta sobrecarga cuando se mueven datos entre SQL Server y el tiempo de ejecución externo, especialmente si los datos se pasan a través de la red en lugar de cargarse directamente desde SQL Server.

Por todas estas razones, no hay ninguna solución única para mitigar este tiempo de carga inicial, como el impacto de rendimiento varía considerablemente dependiendo de la tarea. Por ejemplo, se realiza el almacenamiento en caché para puntuar en lotes; de fila única por lo tanto, las operaciones sucesivas de puntuación son mucho más rápidas y se vuelve a cargar el modelo ni el tiempo de ejecución de R. También puede usar [puntuación nativa](../sql-native-scoring.md) para evitar cargar el runtime de R por completo.

Para entrenar modelos grandes o de puntuación por lotes grande, la sobrecarga puede ser mínima en comparación con las mejoras de evitar el movimiento de datos o de procesamiento paralelo y streaming. Consulte este blog para la Guía de rendimiento adicionales:

+ [Uso de R para detectar el fraude en 1 millón de transacciones por segundo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

Los siguientes son vínculos a información, herramientas y scripts que se usan en el desarrollo de estas pruebas.

+ Pruebas de secuencias de comandos y vínculos a los datos de rendimiento: [Datos de ejemplo y scripts para el estudio de las optimizaciones de SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artículo que describe la solución de coincidencia de reanudación: [Sugerencia para la optimización y trucos para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados en la optimización de SQL para la solución de coincidencia de reanudación: [Repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Obtenga información acerca de la administración de Windows server

+ [Determinar el tamaño apropiado del archivo de paginación para las versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880)

+ [Descripción de NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Cómo SQL Server es compatible con NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Obtenga información sobre las optimizaciones de SQL Server

+ [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introducción a las tablas optimizadas para memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demostración: Mejora del rendimiento de OLTP en memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Deshabilitar compresión de una tabla o un índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Obtenga información sobre la administración de SQL Server

+ [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

+ [Presentación del regulador de recursos](https://technet.microsoft.com/library/bb895232.aspx)

+ [Regulación de recursos para R Services](resource-governance-for-r-services.md)

+ [Cómo crear un grupo de recursos para R](how-to-create-a-resource-pool-for-r.md)

+ [Un ejemplo de configuración del regulador de recursos](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Herramientas

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd) (Herramienta DISKSPD de generador de carga de almacenamiento/prueba de rendimiento)

+ [Referencia de la utilidad FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Otros artículos de esta serie

[Performance tuning para R - Introducción](sql-server-r-services-performance-tuning.md)

[Optimización del rendimiento de R - configuración de SQL Server](sql-server-configuration-r-services.md)

[Optimización del rendimiento de R: R optimización de código y los datos](r-and-data-optimization-r-services.md)

[Los resultados del caso práctico: optimización del rendimiento](performance-case-study-r-services.md)
