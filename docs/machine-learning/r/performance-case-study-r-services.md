---
title: Optimización del rendimiento de los resultados
description: En este artículo se resumen los métodos, los resultados y las conclusiones de dos casos prácticos que han probado varios métodos de optimización.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6afdda3975fc8f6c269f9c1fcbca35318f0c4da
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180004"
---
# <a name="performance-for-r-services-results-and-resources"></a>Rendimiento de R Services: resultados y recursos
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artículo es el cuarto y último de una serie que describe la optimización del rendimiento de R Services. En este artículo se resumen los métodos, los resultados y las conclusiones de dos casos prácticos que han probado varios métodos de optimización.

Los dos casos prácticos tenían objetivos diferentes:

+ El primer caso práctico, presentado por el equipo de desarrollo de R Services, pretendía medir el impacto de técnicas de optimización concretas
+ El segundo caso práctico, realizado por un equipo de científicos de datos, realizaba ensayos de varios métodos para determinar las mejores optimizaciones para un escenario específico de puntuación de gran volumen.

En este tema se presentan los resultados detallados del primer caso práctico. En el segundo caso práctico, un resumen describe las conclusiones generales. Al final de este tema se incluyen vínculos a todos los scripts y datos de ejemplo, así como a los recursos utilizados por los autores originales.

## <a name="performance-case-study-airline-dataset"></a>Caso práctico de rendimiento: Conjunto de datos Airline

Este caso práctico del equipo de desarrollo de SQL Server R Services ha probado los efectos de varias optimizaciones. Se ha creado un único modelo rxLogit y se ha realizado la puntuación en el conjunto de datos Airline. Las optimizaciones se han aplicado durante los procesos de entrenamiento y puntuación para evaluar distintos impactos.

- GitHub: [Scripts y datos de ejemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para el estudio de optimizaciones de SQL Server

### <a name="test-methods"></a>Métodos de prueba

1. El conjunto de datos Airline consta de una sola tabla de 10 millones de filas. Se ha descargado y cargado de forma masiva en SQL Server.
2. Se han realizado seis copias de la tabla.
3. Se han aplicado diversas modificaciones a las copias de la tabla para probar características de SQL Server tales como compresión de página, compresión de fila, indexación, almacén de datos en columnas, etc.
4. El rendimiento se ha medido antes y después de aplicar cada optimización.

| Nombre de la tabla| Descripción|
|------|------|
| *airline* | Datos convertidos desde el archivo xdf original con `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido en entero en lugar de en cadena. También se agrega una columna *rowNum*.|
| *airlineWithIndex*    | Los mismos datos que la tabla *airlineWithIntCol*, pero con un único índice agrupado por medio de la columna *rowNum*.|
| *airlineWithPageComp* | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de página habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineWithRowComp*  | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de fila habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineColumnar*     | Almacén de columnas con un único índice agrupado. Esta tabla se rellena con datos de un archivo csv limpio.|

Cada prueba consta de estos pasos:

1. Antes de cada prueba, se indujo a la recolección de elementos no utilizados de R.
2. Se ha creado un modelo de regresión logística basado en los datos de la tabla. El valor de *rowsPerRead* en cada prueba estaba establecido en 500 000.
3. Las puntuaciones se han generado con el modelo entrenado.
4. Cada prueba se ha ejecutado seis veces. Se ha descartado el tiempo de la primera ejecución (la denominada "ejecución en frío"). Para dar cabida a los valores atípicos ocasionales, también se ha descartado el tiempo **máximo** de las cinco ejecuciones restantes. La media de las cuatro ejecuciones restantes se usó para calcular la media de tiempo de ejecución transcurrido de cada prueba.
5. Las pruebas se han ejecutado con el parámetro *reportProgress* con el valor 3 (= intervalos y progreso de los informes). Cada archivo de salida contiene información relativa al tiempo empleado en E/S, el tiempo de transición y el tiempo de proceso. Estos valores de tiempo son útiles a la hora de solucionar problemas y realizar diagnósticos.
6. La salida de la consola se ha dirigido también a un archivo en el directorio de salida.
7. Los scripts de prueba han procesado los tiempos en estos archivos para calcular el tiempo medio de las ejecuciones.

Por ejemplo, los siguientes resultados corresponden a los tiempos de una sola prueba. Los principales intervalos de interés son **Total read time** (tiempo de E/S) y **Transition time** (sobrecarga al configurar procesos de cálculo).

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

Se recomienda que descargue y modifique los scripts de prueba para ayudarle a solucionar problemas con R Services o con funciones de RevoScaleR.

### <a name="test-results-all"></a>Resultados de la prueba (todos)

En esta sección se comparan los resultados de antes y después de cada una de las pruebas.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamaño de los datos con compresión y un almacén de tablas en columnas

En la primera prueba se ha comparado el uso de compresión y una tabla en columnas para reducir el tamaño de los datos.

| Nombre de la tabla            | Filas     | Reserved   | data       | index_size | No utilizado  | % Saving (reserved) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10 000 000 | 2 978 816 KB | 2 972 160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10 000 000 | 625 784 KB  | 623 744 KB  | 1352 KB    | 688 KB  | 79 %                 |
| *airlineWithRowComp*  | 10 000 000 | 1 262 520 KB | 1 258 880 KB | 2552 KB    | 1088 KB | 58 %                 |
| *airlineColumnar*     | 9 999 999  | 201 992 KB  | 201 624 KB  | N/D        | 368 KB  | 93 %                 |

**Conclusiones**

La mayor reducción del tamaño de los datos se ha obtenido al aplicar un índice de almacén de columnas, seguido de la compresión de página.

#### <a name="effects-of-compression"></a>Efectos de la compresión

En esta prueba se han comparado las ventajas de la compresión de fila, la compresión de página y ninguna compresión. Un modelo se ha entrenado con `rxLinMod` en datos de tres tablas de datos diferentes. Se usó la misma fórmula y la misma consulta en todas las tablas.

| Nombre de la tabla            | Nombre de la prueba       | numTasks | Promedio de tiempo |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5,6775       |
|                       | NoCompression (en paralelo)| 4        | 5,1775       |
| *airlineWithPageComp* | NoCompression | 1        | 6,7875       |
|                       | PageCompression (en paralelo) | 4        | 5,3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6,1325       |
|                       | RowCompression (en paralelo)  | 4        | 5,2375       |

**Conclusiones**

La compresión por sí sola no parece servir de ayuda. En este ejemplo, el aumento de la CPU para controlar la compresión compensa la disminución del tiempo de E/S.

Con todo, cuando la prueba se ejecuta en paralelo estableciendo *numTasks* en 4, el promedio de tiempo disminuye.

En los conjuntos de datos grandes, es posible que el efecto de la compresión sea más evidente. La compresión depende del conjunto de datos y de los valores, por lo que puede que sea necesario experimentar para averiguar el efecto que la compresión tiene en el conjunto de datos.

### <a name="effect-of-windows-power-plan-options"></a>Efecto de las opciones del plan de energía de Windows

En este experimento, `rxLinMod` se usó con la tabla *airlineWithIntCol*. El plan de energía de Windows se estableció en **Equilibrado** o **Alto rendimiento**. En todas las pruebas, *numTasks* se estableció en 1. La prueba se realizó seis veces y se llevó a cabo dos veces con ambas opciones de energía para investigar la variabilidad de los resultados.

Opción de energía **Alto rendimiento**:

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

El tiempo de ejecución es más coherente y más rápido cuando se usa el plan de energía **Alto rendimiento**.

#### <a name="using-integer-vs-strings-in-formulas"></a>Uso de enteros frente a cadenas en fórmulas

Esta prueba evaluó el impacto de la modificación del código de R para evitar un problema común con factores de cadena. En concreto, un modelo se entreno con `rxLinMod` y dos tablas: en la primera, los factores se almacenan como cadenas; en la segunda tabla, los factores se almacenan como enteros.

+ En la tabla *airline*, la columna [DayOfWeek] contiene cadenas. Se usó el parámetro _colInfo_ para especificar los niveles de factor (lunes, martes, etc.)

+  En la tabla *airlineWithIndex*, [DayOfWeek] es un entero. No se especificó el parámetro _colInfo_.

+ En ambos casos, se usó la misma fórmula: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nombre de la tabla          | Nombre de la prueba   | Promedio de tiempo |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10,72        |
| *airlineWithIntCol* | *IntCol*    | 3,4475       |

**Conclusiones**

El uso de enteros en lugar de cadenas como factores no supone una ventaja clara.

### <a name="avoiding-transformation-functions"></a>Elusión de funciones de transformación

En esta prueba, un modelo se entreno con `rxLinMod`, pero el código se cambió entre las dos ejecuciones:

+ En la primera ejecución, se aplicó una función de transformación como parte de la compilación del modelo. 
+ En la segunda ejecución, los valores de la característica se han calculado previamente y están disponibles, por lo que no se requiere ninguna función de transformación.

| Nombre de la prueba             | Promedio de tiempo |
|-----------------------|--------------|
| WithTransformation    | 5,1675       |
| WithoutTransformation | 4,7          |

**Conclusiones**

El tiempo de entrenamiento fue más corto cuando **no** se usó una función de transformación. En otras palabras, el modelo se entrenó más rápidamente al usar columnas que se calculan previamente y persisten en la tabla.

Se espera que el ahorro sea mayor en caso de que haya muchas más transformaciones y el conjunto de datos fuera mayor (\> 100 millones).

### <a name="using-columnar-store"></a>Uso del almacén en columnas

Esta prueba evaluó las ventajas de rendimiento que supone el uso de un almacén de datos en columnas y un índice. El mismo modelo se entrenó con `rxLinMod` y sin transformaciones de datos.

+ En la primera ejecución, la tabla de datos usó un almacén de filas estándar.
+ En la segunda ejecución, se usó un almacén de columnas.

| Nombre de la tabla         | Nombre de la prueba | Promedio de tiempo |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4,555        |

**Conclusiones**

El rendimiento es mejor con el almacén en columnas que con el almacén de filas estándar. Puede esperarse una diferencia considerable de rendimiento en conjuntos de datos más grandes (\> 100 millones).

### <a name="effect-of-using-the-cube-parameter"></a>Efecto del uso del parámetro cube

La finalidad de esta prueba era determinar si la opción de RevoScaleR para usar el parámetro **cube** calculado previamente puede mejorar el rendimiento. Un modelo se entrenó con `rxLinMod` y esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

En la tabla, los factores *DayOfWeek* se almacenan como cadena.

| Nombre de la prueba     | Parámetro Cube | numTasks | Promedio de tiempo | Predicción de una fila (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91,0725      | 9,959204                        |
|               |                | 4        | 44,09        | 9,959204                        |
|               | `cube = T`     | 1        | 21,1125      | 9,959204                        |
|               |                | 4        | 8.08         | 9,959204                        |

**Conclusiones**

El uso del argumento de parámetro cube mejora claramente el rendimiento.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efecto de cambiar maxDepth para los modelos rxDTree

En este experimento, se usó el algoritmo `rxDTree` para crear un modelo en la tabla *airlineColumnar*. En esta prueba *numTasks* se estableció en 4. Se usaron diferentes valores en *maxDepth* para demostrar cómo la modificación de la profundidad del árbol afecta al tiempo de ejecución.

| Nombre de la prueba       | maxDepth | Promedio de tiempo |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10,1975      |
|                 | 2        | 13,2575      |
|                 | 4        | 19,27        |
|                 | 8        | 45,5775      |
|                 | 16       | 339,54       |

**Conclusiones**

A medida que aumenta la profundidad del árbol, aumenta exponencialmente el número total de nodos. El tiempo transcurrido para la creación del modelo también aumentó significativamente.

### <a name="prediction-on-a-stored-model"></a>Predicción en un modelo almacenado

La finalidad de esta prueba era determinar el impacto del rendimiento en la puntuación cuando el modelo entrenado se guarda en una tabla de SQL Server en lugar de generarse como parte del código actualmente en ejecución. A efectos de puntuación, el modelo almacenado se carga desde la base de datos y las predicciones se generan por medio de una trama de datos de una fila en memoria (contexto de proceso local).

Los resultados de la prueba muestran el tiempo necesario para guardar el modelo y el tiempo que se tarda en cargar el modelo y realizar la predicción.

| Nombre de la tabla | Nombre de la prueba | Promedio de tiempo (en entrenar el modelo) | Tiempo en guardar/cargar el modelo|
|------------|------------|------------|------------|
| aerolínea    | SaveModel| 21,59| 2,08|
| aerolínea    | LoadModelAndPredict | | 2,09 (tiempo de la predicción incluido) |

**Conclusiones**

Cargar un modelo entrenado desde una tabla es claramente una forma más rápida de hacer predicciones. Se recomienda que evite crear el modelo y realizar la puntuación en el mismo script.

## <a name="case-study-optimization-for-the-resume-matching-task"></a>Caso práctico: Optimización de la tarea de comparación de currículos

El modelo de comparación de currículos fue desarrollado por el científico de datos de Microsoft Ke Huang para probar el rendimiento del código de R en SQL Server y, con ello, ayudar a los científicos de datos a crear soluciones escalables de nivel empresarial.

### <a name="methods"></a>Métodos

Se usaron los paquetes RevoScaleR y MicrosoftML para entrenar un modelo predictivo en una solución de R compleja que implica grandes conjuntos de valores. Las consultas SQL y el código de R eran idénticos en todas las pruebas. Las pruebas se realizaron en una sola máquina virtual de Azure con SQL Server instalado. Después, el autor comparó la puntuación con y sin las siguientes optimizaciones proporcionadas por SQL Server:

- Tablas en memoria
- Soft-NUMA
- regulador de recursos

Para evaluar el efecto de soft-NUMA en la ejecución de scripts R, el equipo de ciencia de datos probó la solución en una máquina virtual Azure de 20 núcleos físicos. En estos núcleos físicos, se crearon automáticamente cuatro nodos soft-NUMA, de modo que cada nodo contenía cinco núcleos.

Se aplicó la valoración de afinidad de CPU en el escenario de comparación de currículos, con objeto de evaluar el impacto en los trabajos de R. Se han creado cuatro **grupos de recursos de SQL** y **cuatro grupos de recursos externos** y se ha especificado la afinidad de CPU para asegurarse de que se utilizará el mismo conjunto de CPU en cada nodo.

Cada uno de los grupos de recursos se asignó a un grupo de cargas de trabajo diferente para optimizar el uso del hardware. La razón es que la afinidad de CPU y soft-NUMA no puede dividir la memoria física entre los nodos NUMA físicos; por lo tanto, por definición, todos los nodos soft-NUMA que se basan en el mismo nodo físico NUMA deben usar memoria del mismo bloque de memoria del sistema operativo. En otras palabras, no hay afinidad entre la memoria y el procesador.

Se usó el siguiente proceso para crear esta configuración:

1. Se redujo la cantidad de memoria asignada de forma predeterminada a SQL Server.

2. Se crearon otros cuatro grupos para ejecutar los trabajos de R en paralelo.

3. Se crearon cuatro grupos de cargas de trabajo de modo que cada grupo de cargas de trabajo esté asociado a un grupo de recursos.

4. Se reinició Resource Governor con los nuevos grupos de cargas de trabajo y asignaciones.

5. Se creó una función clasificadora definida por el usuario (UDF) para asignar distintas tareas en grupos de cargas de trabajo diferentes.

6. Se actualizó la configuración de Resource Governor para usar la función con los grupos de cargas de trabajo adecuados.

### <a name="results"></a>Results

La configuración que tuvo el mejor rendimiento en el estudio de comparación de currículos es la siguiente:

-   Cuatro grupos de recursos internos (para SQL Server)

-   Cuatro grupos de recursos externos (para trabajos de script externos)

-   Cada grupo de recursos está asociado a un grupo de cargas de trabajo específico

-   Cada grupo de recursos se asigna a diferentes CPU

-   Uso máximo de memoria interna (para SQL Server) = 30 %

-   Cantidad máxima de memoria para su uso en sesiones de R = 70 %

En el modelo de comparación de currículos, el uso de scripts externos era intensivo y no había otros servicios de motor de base de datos en ejecución. Por lo tanto, los recursos asignados a los scripts externos se aumentaron al 70 %, lo que demostró ser la mejor configuración para el rendimiento de los scripts.

A esta configuración se llegó a experimentando con distintos valores. Si utiliza otro hardware u otra solución, es posible que la configuración óptima sea diferente. Experimente siempre para encontrar la mejor configuración en su caso.

En la solución optimizada, se puntuaron 1,1 millones de filas de datos (con 100 características) en menos de 8,5 segundos en un equipo de 20 núcleos. Las optimizaciones mejoraron considerablemente el rendimiento en términos de tiempo de puntuación.

Los resultados también sugieren que el **número de características** tuvo un impacto considerable en el tiempo de puntuación. La mejora era aún más destacada cuando se usaban más características en el modelo de predicción.

Le recomendamos que lea este artículo del blog y el tutorial que lo acompaña para obtener una descripción detallada.

-   [Sugerencias y trucos para la optimización del aprendizaje automático en SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

Muchos usuarios han observado que se produce una pequeña pausa cuando se carga el runtime de R (o Python) por primera vez. Por esta razón, como se describe en estas pruebas, el tiempo de la primera ejecución suele medirse, pero después se descarta. El almacenamiento en caché posterior puede dar lugar a diferencias notables de rendimiento entre la primera y la segunda ejecución. También se produce cierta sobrecarga cuando los datos se mueven entre SQL Server y el runtime externo, especialmente si los datos se pasan a través de la red en lugar de cargarse directamente desde SQL Server.

Por todas estas razones, no existe una sola solución única para reducir este tiempo de carga inicial, ya que el impacto en el rendimiento varía significativamente en función de la tarea. Por ejemplo, el almacenamiento en caché se realiza para la puntuación de fila única en lotes; por lo tanto, las operaciones de puntuación sucesivas son mucho más rápidas y ni el modelo ni el runtime de R se vuelven a cargar. También puede usar [puntuación nativa](../predictions/native-scoring-predict-transact-sql.md) para evitar que el runtime de R se cargue por completo.

En el caso del entrenamiento de modelos grandes, o la puntuación de lotes grandes, la sobrecarga puede ser mínima en comparación con las ventajas de evitar el movimiento de datos o el streaming y el procesamiento paralelo. Consulte esta entrada de blog para obtener más información sobre el rendimiento:

+ [Uso de R para detectar fraudes en 1 millón transacciones por segundo](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Recursos

Los siguientes vínculos enlazan con información, herramientas y scripts que se usan en el desarrollo de este documento.

+ Scripts de prueba de rendimiento y vínculos a los datos: [Scripts y datos de ejemplo para el estudio de optimizaciones de SQL Server](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artículo que describe la solución de comparación de currículos: [Sugerencias y trucos de optimización para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Scripts usados en la optimización de SQL para la solución de comparación de currículos: [Repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)

### <a name="learn-about-windows-server-management"></a>Más información sobre la administración de Windows Server

+ [Determinar el tamaño apropiado del archivo de paginación para las versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880)

+ [Descripción de NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Cómo SQL Server es compatible con NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Más información sobre optimizaciones de SQL Server

+ [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [Introducción a las tablas optimizadas para memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demostración: Mejora de rendimiento de OLTP en memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Deshabilitar compresión de una tabla o un índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Más información sobre la administración de SQL Server

+ [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

+ [Introducción a Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [Ejemplo de configuración de Resource Governor](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Herramientas

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd) (Herramienta DISKSPD de generador de carga de almacenamiento/prueba de rendimiento)

+ [Referencia de la utilidad FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Otros artículos de esta serie

[Optimización del rendimiento de R: introducción](sql-server-r-services-performance-tuning.md)

[Optimización del rendimiento de R: configuración de SQL Server](sql-server-configuration-r-services.md)

[Optimización del rendimiento de R: optimización de datos y de código de R](r-and-data-optimization-r-services.md)

[Optimización del rendimiento: resultados de casos prácticos](performance-case-study-r-services.md)
