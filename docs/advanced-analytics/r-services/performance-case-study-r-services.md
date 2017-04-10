---
title: "Caso pr&#225;ctico de rendimiento (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 6
---
# Caso pr&#225;ctico de rendimiento (R Services)

Para mostrar el efecto de las instrucciones proporcionadas en las secciones anteriores, las pruebas se ejecutaron mediante las tablas del conjunto de datos de compañía aérea. 

## Pruebas y los datos de ejemplo

Hay seis tablas, con 10 millones de filas de cada tabla:

| Nombre de tabla | Description |
| ---------- | ----------- |
| _compañía aérea_ | Convierten datos de archivo original xdf con *rxDataStep*. |
| _airlineWithIntCol_ | *DayOfWeek* convierte un entero en lugar de una cadena. También agrega un *rowNum* columna. |
| _airlineWithIndex_ | Los mismos datos que la *airlineWithIntCol* tabla, pero con un índice agrupado único mediante el *rowNum* columna. |
| _airlineWithPageComp_ | Los mismos datos que la *airlineWithIndex* tabla, pero habilitada la compresión de página. También agrega dos columnas, *CRSDepHour* y *retrasada*, que se calcula a partir de *CRSDepTime* y *ArrDelay*. |
| _airlineWithRowComp_ | Los mismos datos que la *airlineWithIndex* tabla, pero habilitada la compresión de fila. También agrega dos columnas, *CRSDepHour* y *retrasada* que se calcula a partir de *CRSDepTime* y *ArrDelay*. 
| _airlineColumnar_ | Un almacén de columnas con un índice agrupado único. Esta tabla se rellena con datos desde un archivo csv limpiado los archivos. |

Las secuencias de comandos que se usa para realizar las pruebas descritas en esta sección, así como vínculos a los datos de ejemplo utilizados para las pruebas están disponibles en [https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning).

Cada prueba se ejecutó seis veces, se quitó el momento de la primera ejecución (ejecutar, en frío). Para permitir los valores atípicos ocasionales, también se quitó el tiempo máximo para las ejecuciones de cinco restantes. La media de las cuatro ejecuciones restantes se tomó para calcular el tiempo de ejecución transcurrido promedio de cada prueba. Colección de elementos no utilizados de R indujo antes de cada prueba. El valor de *rowsPerRead* para cada prueba se estableció en 500000.

## Tamaño de los datos cuando se usa la compresión y una tabla de almacenamiento en columnas

Éstos son los resultados del uso de la compresión y una tabla en columnas para reducir el tamaño de los datos:

| Nombre de tabla | Filas | Reservado | Data | index_size | No utilizado | % Guardar (reservado) |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| airlineWithIndex | 10000000 | 2978816 KB | 2972160 KB | 6128 KB | 528 KB | 0 |
| airlineWithPageComp | 10000000 | 625784 KB | 623744 KB | 1352 KB | 688 KB | 79% |
| airlineWithRowComp | 10000000 | 1262520 KB | 1258880 KB | 2552 KB | 1088 KB | 58% |
| airlineColumnar | 9999999 | 201992 KB | 201624 KB | n/d | 368 KB | 93% |

## Uso de vs de entero. Cadena de fórmula

En este experimento, `rxLinMod` se utiliza con la tabla de la compañía aérea (donde *DayOfWeek* es una cadena) y *airlineWithIndex* (donde *DayOfWeek* es un entero). Para el primer caso, `colInfo` se utiliza para especificar los niveles de factor (`Monday`, `Tuesday`, ...). Para el segundo, `colInfo` no se ha especificado. En ambos casos, se utiliza la misma fórmula. La fórmula utilizada es `ArrDelay ~ CRSDepTime + DayOfWeek`. Los resultados siguientes se muestra claramente la ventaja de usar cadena de entero vs:

| Nombre de tabla | Nombre de la prueba | Promedio de tiempo |
| ---------- | --------- | ------------ |
| compañía aérea | FactorCol | 10.72 |
| airlineWithIntCol | IntCol | 3.4475 |

## Con la compresión

En este experimento, `rxLinMod` se usó con el *airlineWithIndex*, *airlineWithPageComp*, y *airlineWithRowComp* tablas. Se usó la misma fórmula y consulta para todas las tablas. 

| Nombre de tabla | Nombre de la prueba | numTasks | Promedio de tiempo |
| ---------- | --------- | -------- | ------------ |
| airlineWithIndex | NoCompression | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| airlineWithPageComp | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| airlineWithRowComp | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

Tenga en cuenta que solo la compresión (*numTasks* establecido en 1) no parece ayudar en este ejemplo, como el aumento de la CPU para controlar la compresión compensa la disminución del tiempo de E/S. Sin embargo, cuando la prueba se ejecuta en paralelo estableciendo *numTasks* 4, disminuye el tiempo promedio. Para grandes conjuntos de datos, el efecto de compresión puede ser más evidente. Compresión depende del conjunto de datos y valores, por lo que puede resultar necesario experimentación para determinar la compresión del efecto que tiene en el conjunto de datos.

## Evitar la función de transformación

En este experimento, `rxLinMod` se usa con la tabla de airlineWithIndex con y sin utilizar una función de transformación.  

| Nombre de la prueba | Promedio de tiempo |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

Tenga en cuenta que hay una mejora en el tiempo cuando no se utiliza una función de transformación (con columnas precalculadas y conserva en la tabla). El ahorro será mucho mayor si hay muchas más transformaciones y el conjunto de datos es mayor (> 100M).

## Utilizar el almacén de columnas

En este experimento, `rxLinMod` se utiliza con las tablas airlineWithIndex y airlineColumnar sin utilizar ninguna transformación. Los resultados indican que el almacén de columnas puede realizar mejor que el almacén de filas. Habrá una diferencia significativa del rendimiento en el conjunto de datos mayor (> 100 M).  

| Nombre de tabla | Nombre de la prueba |Promedio de tiempo |
| ---------- | --------- | ------------ |
| airlineWithIndex | Almacén de filas | 4.67 |
| airlineColumnar | ColStore | 4.555 |

## Efecto del parámetro de cubo

En este experimento, `rxLinMod` se usa con la tabla de la compañía aérea donde `DayOfWeek` se almacena como cadena. La fórmula utilizada es `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`. Los resultados muestran que claramente, el uso de `cube` parámetro mejora el rendimiento. 

| Nombre de la prueba | Parámetro de cubo | numTasks | Promedio de tiempo | Una fila predecir (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## Efecto de maxDepth para rxDTree

En este experimento, `rxDTree` se usa con la tabla airlineColumnar. Varios valores diferentes para *maxDepth* se utiliza para mostrar cómo afecta a la complejidad de tiempo de ejecución. A medida que aumenta la profundidad, el número total de nodos aumenta exponencialmente y aumenta considerablemente el tiempo transcurrido. Para esta prueba *numTasks* se establece en 4.

| Nombre de la prueba | maxDepth | Promedio de tiempo |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

## Efecto de la opción de energía

En este experimento, `rxLinMod` se utiliza con la tabla de airlineWithIntCol mientras Windows estaba establecida equilibrado así como de alto rendimiento, opciones de energía. Para todas las pruebas, *numTasks* se estableció en 1. La prueba se ejecutó 6 veces y se realiza dos veces en ambas opciones de energía para demostrar la variabilidad de los resultados al utilizar la opción de energía equilibrada. Los resultados muestran que los números son más coherente y más rápido para la opción de energía de alto rendimiento. 

__Alto rendimiento__ opción de energía:

| Nombre de la prueba | Ejecutar # | Tiempo transcurrido | Promedio de tiempo |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3,57 segundos | &nbsp; |
| &nbsp; | 2 | 3,45 segundos | &nbsp; |
| &nbsp; | 3 | 3,45 segundos | &nbsp; |
| &nbsp; | 4 | 3.55 segundos | &nbsp; |
| &nbsp; | 5 | 3.55 segundos | &nbsp; |
| &nbsp; | 6 | 3,45 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 3,45 segundos | &nbsp; |
| &nbsp; | 2 | 3.53 segundos | &nbsp; |
| &nbsp; | 3 | 3,63 segundos | &nbsp; |
| &nbsp; | 4 | 3,49 segundos | &nbsp; |
| &nbsp; | 5 | 3,54 segundos | &nbsp; |
| &nbsp; | 6 | 3.47 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

__Equilibrio__ opción de energía:

| Nombre de la prueba | Ejecutar # | Tiempo transcurrido | Promedio de tiempo |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 segundos | &nbsp; |
| &nbsp; | 2 | 4.15 segundos | &nbsp; |
| &nbsp; | 3 | 3.77 segundos | &nbsp; |
| &nbsp; | 4 | 5 segundos | &nbsp; |
| &nbsp; | 5 | 3.92 segundos | &nbsp; |
| &nbsp; | 6 | 3,8 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3,82 segundos | &nbsp; |
| &nbsp; | 2 | 3,84 segundos | &nbsp; |
| &nbsp; | 3 | 3,86 segundos | &nbsp; |
| &nbsp; | 4 | 4.07 segundos | &nbsp; |
| &nbsp; | 5 | 4.86 segundos | &nbsp; |
| &nbsp; | 6 | 3,75 segundos | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## Predicción usando un modelo almacenado

En este experimento, un modelo se crea y se almacena en una base de datos. A continuación, se carga el modelo almacenado en la base de datos y predicciones creadas mediante una trama de datos de una fila en la memoria (contexto de cálculo local). A continuación se muestra el tiempo necesario para entrenar, guardar, cargar el modelo y predecir. Esto es claramente una manera más rápida de realizar una predicción. Los resultados de pruebas muestran el tiempo para guardar el modelo y el tiempo necesario para cargar el modelo y predicción. 

| Nombre de tabla | Nombre de la prueba | Promedio de tiempo (para entrenar el modelo) | Tiempo para guardar/cargar modelo |
| ---------- | --------- | ----- | ----- |
| compañía aérea | Modelo de almacenamiento | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09 (incluye el tiempo para predecir) |


## Solución de problemas de rendimiento

Las pruebas que se utilizan en esta sección generan archivos de salida para cada ejecución utilizando la *reportProgress* parámetro, que se pasa a las pruebas con el valor `3`. El resultado de la consola se dirige a un archivo en el directorio de salida. El archivo de salida contiene información sobre el tiempo empleado en E/S, el tiempo de transición y tiempo de proceso. Estos tiempos son útiles para solucionar problemas y diagnóstico. Estos tiempos para las diversas ejecuciones de proponer el tiempo medio en ejecuciones de proceso de las secuencias de comandos de prueba. Estos scripts de prueba y técnicas también pueden ser útiles para solucionar problemas de problemas al utilizar funciones analíticas de rx en su [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Por ejemplo, a continuación muestra para una serie de muestras. Los intervalos principales de interés son totales leer IO (hora) y transición sobrecarga del tiempo (en configuración de procesos de cálculo).

    Running IntCol Test. Using airlineWithIntCol table.  
        run  1  took  3.66  seconds  
        run  2  took  3.44  seconds  
        run  3  took  3.44  seconds  
        run  4  took  3.44  seconds  
        run  5  took  3.45  seconds  
        run  6  took  3.75  seconds  

    Average Time:  3.4425  
                    metric   time    pct 
    1           Total time 3.4425 100.00 
    2 Overall compute time 2.8512  82.82 
    3      Total read time 2.5378  73.72 
    4      Transition time 0.5913  17.18 
    5    Total non IO time 0.3134   9.10 
 
 ## Vea también
 [Guía de optimización de rendimiento de SQL Server R servicios](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [Configuración de SQL Server para los servicios de R](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R y optimización de datos](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)