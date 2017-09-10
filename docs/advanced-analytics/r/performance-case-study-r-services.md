---
title: Rendimiento de los servicios de R - resultados y los recursos | Documentos de Microsoft
ms.custom: 
ms.date: 07/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f14e3d744a6d65891f6162bf63e69d682d08a971
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="performance-for-r-services-results-and-resources"></a>Rendimiento de los servicios de R: resultados y recursos

En este artículo es el cuarto y final de una serie que describe la optimización del rendimiento para R Services. Este artículo resumen los métodos, resultados y conclusiones de dos casos prácticos que probar distintos métodos de optimización.

Los dos casos prácticos tenía distintos objetivos:

+ El primer caso práctico, el equipo de desarrollo de R Services busca medir el impacto de técnicas de optimización específica
+ El segundo caso práctico, por un equipo de científicos de datos experimentado con varios métodos para determinar las mejores optimizaciones para un escenario concreto de puntuación de gran volumen.

Este tema enumeran los resultados detallados del primer caso práctico. Para el segundo caso práctico, un resumen describe las conclusiones generales. Al final de este tema, encontrará vínculos a todos los scripts y los datos de ejemplo y los recursos usados por los autores originales.

## <a name="performance-case-study-airline-dataset"></a>Caso práctico de rendimiento: conjunto de datos Airline

Este caso práctico en el equipo de desarrollo de SQL Server R Services para probar los efectos de varias optimizaciones. Se creó un modelo único rxLogit y puntuación realiza en el conjunto de datos Airline. Las optimizaciones se aplicaron durante el entrenamiento y puntuación procesos para evaluar el impacto individual.

- Github: [scripts y datos de ejemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning) para su estudio de optimizaciones de SQL Server

### <a name="test-methods"></a>Métodos de prueba

1. El conjunto de datos Airline consiste en una única tabla de M 10 filas. Se ha descargado y carga masiva en SQL Server.
2. Se realizaron seis copias de la tabla.
3. Varias de las modificaciones se aplicaron a las copias de la tabla, para probar las características de SQL Server como la compresión de página, la compresión row, indización, el almacén de datos en columnas, etcetera.
4. Se midió rendimiento antes y después de que se aplica cada optimización.

| Nombre de la tabla| Description|
|------|------|
| *airline* | Datos convertidos desde el archivo xdf original con `rxDataStep`|                          |
| *airlineWithIntCol*   | *DayOfWeek* convertido en entero en lugar de en cadena. También se agrega una columna *rowNum*.|
| *airlineWithIndex*    | Los mismos datos que la tabla *airlineWithIntCol*, pero con un único índice agrupado por medio de la columna *rowNum*.|
| *airlineWithPageComp* | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de página habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineWithRowComp*  | Los mismos datos que la tabla *airlineWithIndex*, pero con la compresión de fila habilitada. También se agregan dos columnas, *CRSDepHour* y *Late*, que se calculan a partir de *CRSDepTime* y *ArrDelay*. |
| *airlineColumnar*     | Almacén de columnas con un único índice agrupado. Esta tabla se rellena con datos de un archivo csv limpio.|

Cada prueba consistió en estos pasos:

1. Antes de cada prueba, se indujo a la recolección de elementos no utilizados de R.
2. Se creó un modelo de regresión logística en función de los datos de tabla. El valor de *rowsPerRead* en cada prueba estaba establecido en 500 000.
3. Las puntuaciones se generaron mediante el modelo de aprendizaje
4. Cada prueba se ejecutó seis veces. Se quitó el momento de la primera ejecución (la "ejecución frío"). Para permitir los valores atípicos ocasional, el **máximo** también se quitó el tiempo entre las ejecuciones de cinco restantes. La media de las cuatro ejecuciones restantes se usó para calcular la media de tiempo de ejecución transcurrido de cada prueba.
5. Las pruebas se ejecutaron con el *reportProgress* parámetro con el valor 3 (= los intervalos de informes y el progreso). Cada archivo de salida contiene información sobre el tiempo empleado en E/S, el tiempo de transición y tiempo de proceso. Estos valores de tiempo son útiles a la hora de solucionar problemas y realizar diagnósticos.
6. La salida de la consola también se dirige a un archivo en el directorio de salida.
7. Los scripts de prueba procesan las horas en estos archivos para calcular el tiempo medio en ejecuciones.

Por ejemplo, los siguientes resultados son las horas comprendidas desde una única prueba. Los principales intervalos de interés son **Total read time** (tiempo de E/S) y **Transition time** (sobrecarga al configurar procesos de cálculo).

**Intervalos de ejemplo**

```
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

Recomendamos que descargue y modifique los scripts de prueba para ayudarle a solucionar problemas con R Services o con funciones de RevoScaleR.

### <a name="test-results-all"></a>Probar los resultados (todos)

Esta sección se comparan antes y después de resultados para cada una de las pruebas.

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>Tamaño de los datos con la compresión y un almacén de columnas de tabla

La primera prueba compara el uso de compresión y una tabla de columna para reducir el tamaño de los datos.

| Nombre de la tabla            | Filas     | Reservado   | Datos       | index_size | No utilizado  | % Saving (reserved) |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10 000 000 | 2 978 816 KB | 2 972 160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10 000 000 | 625 784 KB  | 623 744 KB  | 1352 KB    | 688 KB  | 79 %                 |
| *airlineWithRowComp*  | 10 000 000 | 1 262 520 KB | 1 258 880 KB | 2552 KB    | 1088 KB | 58 %                 |
| *airlineColumnar*     | 9 999 999  | 201 992 KB  | 201 624 KB  | n/d        | 368 KB  | 93 %                 |

**Conclusiones**

La reducción de mayor tamaño de datos que se ha realizado mediante la aplicación de un índice de almacén de columnas, seguido de compresión de página.

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

Compresión por sí sola no parece ayudar a. En este ejemplo, el aumento de la CPU para controlar la compresión compensa la disminución del tiempo de E/S.

Con todo, cuando la prueba se ejecuta en paralelo estableciendo *numTasks* en 4, el promedio de tiempo disminuye.

En los conjuntos de datos grandes, es posible que el efecto de la compresión sea más evidente. La compresión depende del conjunto de datos y de los valores, por lo que puede que sea necesario experimentar para averiguar el efecto que la compresión tiene en el conjunto de datos.

### <a name="effect-of-windows-power-plan-options"></a>Efecto de las opciones del plan de energía de Windows

En este experimento, `rxLinMod` se usó con la tabla *airlineWithIntCol*. El Plan de energía de Windows se ha establecido en **equilibrada** o **de alto rendimiento**. En todas las pruebas, *numTasks* se estableció en 1. La prueba se ejecutó seis veces y se realiza dos veces en ambas opciones de energía para investigar la variabilidad de los resultados.

**Alto rendimiento** opción de energía:

| Nombre de la prueba | Ejecutar\# | Tiempo transcurrido | Promedio de tiempo |
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

| Nombre de la prueba | Ejecutar\# | Tiempo transcurrido | Promedio de tiempo |
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

El tiempo de ejecución es más coherente y más rápida al utilizar las ventanas **de alto rendimiento** plan de energía.

#### <a name="using-integer-vs-strings-in-formulas"></a>Utilizar entero frente a las cadenas en fórmulas

Esta prueba evalúa el efecto de modificar el código de R para evitar un problema común con factores de cadena. En concreto, un modelo se entrenó con `rxLinMod` con dos tablas: en la primera, factores se almacenan como cadenas; en la segunda tabla, factores se almacenan como enteros.

+ Para el *airline* tabla, la columna [DayOfWeek] contiene cadenas. El _colInfo_ parámetro se utiliza para especificar los niveles de factor (lunes, el martes,...)

+  Para el *airlineWithIndex* tabla, [DayOfWeek] es un entero. El _colInfo_ no se especificó un parámetro.

+ En ambos casos, se usó la misma fórmula: `ArrDelay ~ CRSDepTime + DayOfWeek`.

| Nombre de la tabla          | Nombre de la prueba   | Promedio de tiempo |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10,72        |
| *airlineWithIntCol* | *IntCol*    | 3,4475       |

**Conclusiones**

Hay una ventaja evidente cuando usa enteros en lugar de cadenas de factores.

### <a name="avoiding-transformation-functions"></a>Evitar las funciones de transformación

En esta prueba, un modelo se entrenó con `rxLinMod`, pero se cambió el código entre las dos ejecuciones:

+ En la primera ejecución, una función de transformación se aplica como parte de la compilación del modelo. 
+ En la segunda ejecución, los valores de características eran precalculadas y está disponible, por lo que no era necesaria ninguna función de transformación.

| Nombre de la prueba             | Promedio de tiempo |
|-----------------------|--------------|
| WithTransformation    | 5,1675       |
| WithoutTransformation | 4,7          |

**Conclusiones**

Tiempo de entrenamiento fue cuando más corto **no** utilizando una función de transformación. En otras palabras, el modelo se entrenó con mayor rapidez al usar las columnas que se calcula previamente y se almacenan en la tabla.

El ahorro que se espera debe ser mayor si hubo muchos más transformaciones y el conjunto de datos fuesen de mayor tamaño (\> 100 M).

### <a name="using-columnar-store"></a>Uso del almacén de columna

Esta prueba evalúa las ventajas de rendimiento de usar un almacén de datos en columnas y el índice. El mismo modelo se entrenó con `rxLinMod` y ninguna transformación de datos.

+ En la primera ejecución, la tabla de datos utiliza un almacén de filas estándar.
+ En la segunda ejecución, se utiliza un almacén de columnas.

| Nombre de la tabla         | Nombre de la prueba | Promedio de tiempo |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4,67         |
| *airlineColumnar*  | ColStore  | 4,555        |

**Conclusiones**

El rendimiento es mejor con el almacén de columna que con el almacén de filas estándar. Se puede esperar una diferencia significativa del rendimiento en conjuntos de datos mayores (\> 100 M).

### <a name="effect-of-using-the-cube-parameter"></a>Efecto de usar el parámetro de cubo

El objetivo de esta prueba era determinar si la opción de RevoScaleR para usar el precalculadas **cubo** parámetro puede mejorar el rendimiento. Un modelo se entrenó con `rxLinMod`, utilizando esta fórmula:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

En la tabla, los factores *DayOfWeek* se almacena como una cadena.

| Nombre de la prueba     | Parámetro Cube | numTasks | Promedio de tiempo | Fila única predecir (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91,0725      | 9,959204                        |
|               |                | 4        | 44,09        | 9,959204                        |
|               | `cube = T`     | 1        | 21,1125      | 9,959204                        |
|               |                | 4        | 8,08         | 9,959204                        |

**Conclusiones**

El uso del argumento de parámetro de cubo claramente mejora el rendimiento.

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>Efecto del cambio maxDepth para los modelos de rxDTree

En este experimento, el `rxDTree` algoritmo se utilizó para crear un modelo en el *airlineColumnar* tabla. En esta prueba *numTasks* se estableció en 4. Varios valores diferentes para *maxDepth* se utiliza para mostrar cómo modificar la profundidad de árbol afecta al tiempo de ejecución.

| Nombre de la prueba       | maxDepth | Promedio de tiempo |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10,1975      |
|                 | 2        | 13,2575      |
|                 | 4        | 19,27        |
|                 | 8        | 45,5775      |
|                 | 16       | 339,54       |

**Conclusiones**

A medida que aumenta la profundidad del árbol, se aumenta exponencialmente el número total de nodos. El tiempo transcurrido para crear el modelo también aumenta significativamente.

### <a name="prediction-on-a-stored-model"></a>Predicciones en un modelo almacenado

El propósito de esta prueba era determinar el impacto de rendimiento de puntuación cuando el modelo entrenado se guarda en una tabla de SQL Server en lugar de genera como parte del código está ejecutando actualmente. Para puntuar, el modelo almacenado se carga desde la base de datos y las predicciones se crean mediante una trama de datos de una fila en la memoria (contexto de proceso local).

Los resultados de pruebas muestran el momento de guardar el modelo y el tiempo necesario para cargar el modelo y realizar predicciones.

| Nombre de la tabla | Nombre de la prueba | Promedio de tiempo (en entrenar el modelo) | Tiempo en guardar/cargar el modelo|
|------------|------------|------------|------------|
| airline    | SaveModel| 21,59| 2,08|
| airline    | LoadModelAndPredict | | 2,09 (tiempo de la predicción incluido) |

**Conclusiones**

Cargar un modelo entrenado desde una tabla es claramente un modo más rápido realizar la predicción. Se recomienda que evite crear el modelo y la realización de puntuación en la misma secuencia de comandos.

## <a name="case-study-optimization-for-resume-matching-task"></a>Caso práctico: optimización para reanudar la tarea de búsqueda de coincidencias

El modelo de coincidencia de reanudación fue desarrollado por científicos de datos de Microsoft Ke Huang para probar el rendimiento del código R en SQL Server y habilitar los científicos de datos admitir soluciones escalables y de nivel de empresa.

### <a name="methods"></a>Métodos

Los paquetes RevoScaleR y de MicrosoftML se usaron para entrenar un modelo de predicción en una solución de R complejo que implican grandes conjuntos de datos. Las consultas SQL y código de R son idénticos. Todas las pruebas se realizaron en una sola máquina virtual de Azure con SQL Server instalado. El autor, a continuación, en comparación con tiempos de puntuación con y sin estas optimizaciones proporcionadas por SQL Server:

- Tablas en memoria
- Soft-NUMA
- Regulador de recursos

Para evaluar el efecto de NUMA de software en la ejecución del script de R, el equipo de ciencia de datos probado la solución en una máquina virtual con 20 núcleos físicos. En estos núcleos físicos, cuatro nodos NUMA de software se crearon automáticamente, tal que cada nodo contiene cinco núcleos.

Afinamiento de CPU se aplica en el escenario de coincidencia de reanudación, para evaluar el impacto sobre los trabajos de R. Cuatro **grupos de recursos SQL** y cuatro **grupos de recursos externos** fueron creadas, y no se especificó la afinidad de CPU para asegurarse de que se utilizaría el mismo conjunto de CPU en cada nodo.

Cada uno de los grupos de recursos se asignó a un grupo de cargas de trabajo diferente, para optimizar el uso de hardware. El motivo es que Soft-NUMA y afinidad de CPU no puede dividir la memoria física en los nodos NUMA físicos; por lo tanto, por definición todos los nodos NUMA automáticos que se basan en el mismo nodo NUMA físico deben usar memoria en el mismo bloque de memoria de sistema operativo. En otras palabras, no hay ninguna afinidad de procesador de memoria.

El siguiente proceso se usó para crear esta configuración:

1. Reducir la cantidad de memoria asignada de forma predeterminada en SQL Server.

2. Cree cuatro grupos nuevos para ejecutar los trabajos de R en paralelo.

3. Cree cuatro grupos de cargas de trabajo de forma que cada grupo de cargas de trabajo está asociado a un grupo de recursos.

4. Reinicie el regulador de recursos con los nuevos grupos de cargas de trabajo y las asignaciones.

5. Crear una función clasificadora definida por el usuario (UDF) para asignar diferentes tareas en los grupos de cargas de trabajo diferente.

6. Actualizar la configuración del regulador de recursos para usar la función para los grupos de cargas de trabajo adecuado.

### <a name="results"></a>Resultado

La configuración que tenía el mejor rendimiento en la coincidencia de reanudación estudiar fue el siguiente:

-   Cuatro grupos de recursos internos (para SQL Server)

-   Cuatro grupos de recursos externos (para los trabajos de script externo)

-   Cada grupo de recursos está asociado a un grupo de cargas de trabajo concreto

-   Cada grupo de recursos se asigna a las distintas CPU

-   Uso máximo de memoria interna (para SQL Server) = 30%

-   Cantidad máxima de memoria para su uso en las sesiones de R = 70%

Para el modelo de coincidencia de reanudación, el uso de script externo fue elevado y no hay ninguna otra base de datos servicios del motor de ejecución. Por lo tanto, los recursos asignados a los scripts externos se incrementó al 70%, lo que era la mejor configuración para el rendimiento de la secuencia de comandos.

Esta configuración se ha llegado a experimentar con valores diferentes. Si usa hardware diferente o una solución distinta, la configuración óptima podría ser diferente.

> [!IMPORTANT]
> Experimento para determinar la mejor configuración para su caso.

En la solución optimizada, se puntúan 1.1 millones de filas de datos (con 100 características) en menos de 8,5 segundos en un equipo de 20 núcleos. Optimizaciones de mejorar considerablemente el rendimiento en términos de tiempo de puntuación.

Los resultados también sugieren que la **número de características** tenido un impacto significativo en la hora de puntuación. La mejora era incluso más importancia cuando se utilizaban más características en el modelo de predicción.

Le recomendamos que lea este artículo de blog y el tutorial que lo acompañan para obtener información detallada.

-   [Sugerencias de optimización y trucos para el aprendizaje automático en SQL Server](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

## <a name="resources"></a>Recursos

Los siguientes son vínculos a información, herramientas y scripts usados en el desarrollo de estas pruebas.

+ Secuencias de comandos y vínculos a los datos de la prueba de rendimiento: [secuencias de comandos para su estudio de optimizaciones de SQL Server y datos de ejemplo](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ Artículo que describe la solución de coincidencia de reanudación: [sugerencia para la optimización y trucos para SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ Secuencias de comandos utilizadas en la optimización de SQL para la solución de coincidencia de reanudación: [repositorio de GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>Obtenga información sobre la administración de Windows server

+ [Determinar el tamaño apropiado del archivo de paginación para las versiones de 64 bits de Windows](https://support.microsoft.com/kb/2860880)

+ [Descripción NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [Cómo SQL Server es compatible con NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [NUMA de software](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>Obtenga información acerca de las optimizaciones de SQL Server

+ [Reorganizar y volver a generar índices](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [Introducción a las tablas optimizadas en memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [Demostración: Mejora de rendimiento de OLTP en memoria](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Compresión de datos](../../relational-databases/data-compression/data-compression.md)

+ [Habilitar compresión de una tabla o un índice](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [Deshabilitar compresión de una tabla o un índice](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>Obtenga información sobre la administración de SQL Server

+ [Supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

+ [Introducción a regulador de recursos](https://technet.microsoft.com/library/bb895232.aspx)

+ [Regulación de recursos para R Services](resource-governance-for-r-services.md)

+ [Cómo crear un grupo de recursos para R](how-to-create-a-resource-pool-for-r.md)

+ [Un ejemplo de cómo configurar el regulador de recursos](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>Herramientas

+ [DISKSPD storage load generator/performance test tool](https://github.com/microsoft/diskspd) (Herramienta DISKSPD de generador de carga de almacenamiento/prueba de rendimiento)

+ [Referencia de la utilidad FSUtil](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>Otros artículos de esta serie

[Rendimiento para la optimización de R: Introducción](sql-server-r-services-performance-tuning.md)

[Ajuste del rendimiento de R - configuración de SQL Server](sql-server-configuration-r-services.md)

[Ajuste del rendimiento de R - R optimización del código y los datos](r-and-data-optimization-r-services.md)

[Ajuste del rendimiento: resultados del estudio de caso](performance-case-study-r-services.md)

