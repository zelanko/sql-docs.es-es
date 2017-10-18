---
title: Procesamiento de consultas adaptable en bases de datos de Microsoft SQL | Microsoft Docs | Microsoft Docs
description: "Características de procesamiento de consultas adaptable para mejorar el rendimiento de las consultas en SQL Server (2017 y versiones posteriores) y Azure SQL Database."
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: 
ms.assetid: 
author: joesackmsft
ms.author: josack;monicar
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 246ea9f306c7d99b835c933c9feec695850a861b
ms.openlocfilehash: e2bbfc9a89d4ec2dd3cce5625adfb09c7f85efbe
ms.contentlocale: es-es
ms.lasthandoff: 10/13/2017

---

# <a name="adaptive-query-processing-in-sql-databases"></a>Procesamiento de consultas adaptable en bases de datos SQL

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

En este artículo se presentan las características de procesamiento de consultas adaptable que se pueden usar para mejorar el rendimiento de las consultas en SQL Server y Azure SQL Database:
- Comentarios de concesión de memoria de modo de proceso por lotes.
- Combinación adaptable de modo de proceso por lotes.
- Ejecución intercalada. 

En general, SQL Server ejecuta una consulta del modo siguiente:
1. El proceso de optimización de consultas genera un conjunto de planes de ejecución factibles para una consulta concreta. Durante este tiempo se calcula el costo de las opciones del plan y se usa el plan con el menor costo estimado.
1. El proceso de ejecución de consultas toma el plan elegido por el optimizador de consultas y lo usa para la ejecución.
    
A veces el plan elegido por el optimizador de consultas no es óptimo por una serie de motivos. Por ejemplo, el número estimado de filas que pasan por el plan de consulta puede ser incorrecto. Los costos estimados ayudan a determinar el plan que se selecciona para la ejecución. Si las estimaciones de cardinalidad son incorrectas, se sigue usando el plan original a pesar de los deficientes supuestos originales.

![Características de procesamiento de consultas adaptable](./media/1_AQPFeatures.png)

### <a name="how-to-enable-adaptive-query-processing"></a>Cómo habilitar el procesamiento de consultas adaptable
Puede hacer que las cargas de trabajo sean aptas automáticamente para el procesamiento de consultas adaptable si habilita el nivel de compatibilidad 140 para la base de datos.  Puede establecerlo con Transact-SQL. Por ejemplo:
```sql
ALTER DATABASE [WideWorldImportersDW] SET COMPATIBILITY_LEVEL = 140;
```
## <a name="batch-mode-memory-grant-feedback"></a>Comentarios de concesión de memoria de modo de proceso por lotes
El plan posterior a la ejecución de una consulta en SQL Server incluye la memoria mínima necesaria para la ejecución y el tamaño de concesión de memoria ideal para que todas las filas quepan en la memoria. El rendimiento se ve afectado si los tamaños de concesión de memoria son incorrectos. A su vez, unas concesiones excesivas se traducen en memoria desperdiciada y en simultaneidad reducida. Las concesiones de memoria insuficientes provocan un costoso desbordamiento en disco. Al ocuparse de las cargas de trabajo repetidas, los comentarios de concesión de memoria de modo de proceso por lotes vuelven a calcular la memoria real necesaria para una consulta y luego actualizan el valor de la concesión del plan almacenado en caché.  Cuando se ejecuta una instrucción de consulta idéntica, la consulta usa el tamaño de concesión de memoria revisado, con lo que se reducen las concesiones de memoria excesivas que afectan a la simultaneidad y se solucionan las concesiones de memoria subestimadas que provocan costosos desbordamientos en disco.
El gráfico siguiente muestra un ejemplo de uso de los comentarios de concesión de memoria adaptable de modo de proceso por lotes. Para la primera ejecución de la consulta, la duración es de *88 segundos*, debido a los grandes desbordamientos:
```sql
DECLARE @EndTime datetime = '2016-09-22 00:00:00.000';
DECLARE @StartTime datetime = '2016-09-15 00:00:00.000';
SELECT TOP 10 hash_unique_bigint_id
FROM dbo.TelemetryDS
WHERE Timestamp BETWEEN @StartTime and @EndTime
GROUP BY hash_unique_bigint_id
ORDER BY MAX(max_elapsed_time_microsec) DESC;
```
![Grandes desbordamientos](./media/2_AQPGraphHighSpills.png)

Con los comentarios de concesión de memoria habilitados para la segunda ejecución, la duración es de *1 segundo* (partiendo de 88 segundos), los desbordamientos se eliminan por completo y la concesión es superior: 

![Sin desbordamientos](./media/3_AQPGraphNoSpills.png)

### <a name="memory-grant-feedback-sizing"></a>Tamaño de los comentarios de concesión de memoria
*En el caso de las concesiones excesivas*, si la memoria concedida es más de dos veces el tamaño de la memoria usada real, los comentarios de concesión de memoria volverán a calcular la concesión de memoria y actualizarán el plan almacenado en caché.  Los planes con concesiones de memoria por debajo de 1 MB no se vuelven a calcular para usos por encima del límite.
*En el caso de las concesiones de memoria de tamaño insuficiente* que provocan un desbordamiento en disco para operadores de modo de proceso por lotes, los comentarios de concesión de memoria desencadenarán un nuevo cálculo de la concesión de memoria. Los eventos de desbordamiento se notifican a los comentarios de concesión de memoria y se pueden mostrar a través del evento de XEvent *spilling_report_to_memory_grant_feedback*. Este evento devuelve el identificador de nodo del plan y el tamaño de los datos desbordados de ese nodo.

### <a name="memory-grant-feedback-and-parameter-sensitive-scenarios"></a>Comentarios de concesión de memoria y escenarios confidenciales de parámetros
Los distintos valores de parámetros también pueden necesitar diferentes planes de consulta para seguir siendo óptimos. Este tipo de consulta se define como "sensible a parámetros". En el caso de los planes sensibles a parámetros, los comentarios de concesión de memoria se deshabilitarán en una consulta si esta tiene requisitos de memoria inestables.  El plan se deshabilita tras varias ejecuciones repetidas de la consulta, cosa que se puede observar mediante la supervisión del evento de XEvent *memory_grant_feedback_loop_disabled*.

### <a name="memory-grant-feedback-caching"></a>Almacenamiento en caché de los comentarios de concesión de memoria
Los comentarios pueden almacenarse en el plan almacenado en caché para una sola ejecución. Pero son las ejecuciones consecutivas de esa instrucción las que se benefician de los ajustes de los comentarios de concesión de memoria. Esta característica se aplica a la ejecución repetida de instrucciones. Los comentarios de concesión de memoria solo cambian el plan almacenado en caché. De momento los cambios no se capturan en la consulta Ssore.
Si el plan se elimina de la memoria caché, no se conservan los comentarios. Los comentarios también se pierden si se produce una conmutación por error. Una instrucción con OPTION(RECOMPILE) crea un plan y no lo almacena en caché. Puesto que no se almacena, no se generan comentarios de concesión de memoria y no se almacenan para esa compilación y ejecución.  Pero si una instrucción equivalente (es decir, con el mismo hash de consulta) que *no* ha usado OPTION(RECOMPILE) se ha almacenado en caché y luego se ha vuelto a ejecutar, la instrucción consecutiva puede beneficiarse de los comentarios de concesión de memoria.

### <a name="tracking-memory-grant-feedback-activity"></a>Seguimiento de la actividad de los comentarios de concesión de memoria
Puede realizar un seguimiento de los eventos de comentarios de concesión de memoria mediante el evento de XEvent *memory_grant_updated_by_feedback*.  Este evento realiza un seguimiento del historial de recuentos de ejecución actual, del número de veces que los comentarios de concesión de memoria han provocado una actualización del plan, de la concesión de memoria adicional ideal antes de la modificación y de la concesión de memoria adicional ideal después de que los comentarios de concesión de memoria hayan modificado el plan almacenado en caché.

### <a name="memory-grant-feedback-resource-governor-and-query-hints"></a>Comentarios de concesión de memoria, regulador de recursos y sugerencias de consulta
La memoria real concedida respeta el límite de memoria de consulta determinado por el regulador de recursos o la sugerencia de consulta.

## <a name="batch-mode-adaptive-joins"></a>Combinaciones adaptables de modo de proceso por lotes
La característica de combinaciones adaptables de modo de proceso por lotes posibilita la elección de una combinación hash o un método de combinación de bucle anidado que se retrasa hasta *después* de que se haya analizado la primera entrada.  El operador de combinación adaptable define un umbral que se usa para decidir cuándo cambiar a un plan de bucle anidado. El plan, por tanto, puede cambiar de forma dinámica para una mejor estrategia de combinación durante la ejecución.
Funcionamiento:
- Si el recuento de filas de la entrada de combinación de compilación es lo suficientemente pequeño como para que una combinación de bucle anidado sea más adecuada que una combinación hash, el plan cambia a un algoritmo de bucle anidado.
- Si la entrada de combinación de compilación supera un umbral de recuento de filas determinado, no se produce ningún cambio y el plan continúa con una combinación hash.

La siguiente consulta se usa para mostrar un ejemplo de combinación adaptable:

```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE   [fo].[Quantity] = 360;
```

La consulta devuelve 336 filas.  Al habilitar las estadísticas de consultas activas se ve el siguiente plan:

![La consulta da lugar a 336 filas](./media/4_AQPStats336Rows.png)

En el plan se ve lo siguiente:
1. Hay una exploración de índice de almacén de columnas que se usa para proporcionar filas para la fase de compilación de combinación hash.
1. Hay un nuevo operador de combinación adaptable. Este operador define un umbral que se usa para decidir cuándo cambiar a un plan de bucle anidado.  En el ejemplo, el umbral es 78 filas.  Todo lo que tenga &gt; = 78 filas usará una combinación hash.  Si es inferior al umbral, se usará una combinación de bucle anidado.
1. Puesto que se devuelven 336 filas, se supera el umbral y la segunda rama representa la fase de sondeo de una operación de combinación hash estándar. Observe que las estadísticas de consultas activas muestran las filas que pasan por los operadores: en este caso "672 de 672".
1. La última rama es la búsqueda en índice clúster que usa la combinación de bucle anidado si no se ha superado el umbral. Observe que se ve "0 de 336" filas mostradas (la rama no se usa).
 Ahora vamos a comparar el plan con la misma consulta, pero esta vez para un valor de cantidad que solo tiene una fila en la tabla:
 
```sql
SELECT  [fo].[Order Key], [si].[Lead Time Days],
[fo].[Quantity]
FROM    [Fact].[Order] AS [fo]
INNER JOIN [Dimension].[Stock Item] AS [si]
       ON [fo].[Stock Item Key] = [si].[Stock Item Key]
WHERE   [fo].[Quantity] = 361;
```
La consulta devuelve una fila.  Al habilitar las estadísticas de consultas activas se ve el siguiente plan:

![La consulta da lugar a una fila](./media/5_AQPStatsOneRow.png)

En el plan se ve lo siguiente:
- Con una fila devuelta, puede ver que por la búsqueda en índice clúster ahora pasan filas.
- Y puesto que no se ha continuado con la fase de compilación de combinación hash, se verán cero filas que pasan por la segunda rama.

### <a name="adaptive-join-benefits"></a>Ventajas de la combinación adaptable
La cargas de trabajo con oscilaciones frecuentes entre análisis de entrada de combinación pequeños y grandes son las que más se benefician de esta característica.

### <a name="adaptive-join-overhead"></a>Sobrecarga de la combinación adaptable
Las combinaciones adaptables tienen unos requisitos de memoria superiores a un plan equivalente de combinación de bucle anidado de índice. La memoria adicional se solicita como si el bucle anidado fuera una combinación hash. También hay sobrecarga para la fase de compilación como una operación de detención e inicio frente a una combinación equivalente de transmisión de bucle anidado. Ese costo adicional va acompañado de flexibilidad en escenarios donde los recuentos de filas pueden fluctuar en la entrada de compilación.

### <a name="adaptive-join-caching-and-re-use"></a>Almacenamiento en caché y reutilización de combinación adaptable
Las combinaciones adaptables de modo de proceso por lotes funcionan para la ejecución inicial de una instrucción y, una vez compiladas, las ejecuciones consecutivas seguirán siendo adaptables según el umbral de combinación adaptable compilado y las filas de runtime que pasan a través de la fase de compilación de la entrada externa.

### <a name="tracking-adaptive-join-activity"></a>Seguimiento de la actividad de combinación adaptable
El operador de combinación adaptable tiene los siguientes atributos de operador de plan:

| Atributo de plan | Description |
|--- |--- |
| AdaptiveThresholdRows | Muestra el uso de umbral para cambiar de una combinación hash a una combinación de bucle anidado. |
| EstimatedJoinType | El tipo de combinación probable. |
| ActualJoinType | En un plan real, se muestra qué algoritmo de combinación se ha elegido finalmente según el umbral. |

El plan estimado muestra la forma del plan de combinación adaptable, junto con un umbral de combinación adaptable definido y un tipo de combinación estimado.

### <a name="adaptive-join-and-query-store-interoperability"></a>Combinación adaptable e interoperabilidad del Almacén de consultas
El Almacén de consultas captura y puede aplicar un plan de combinación adaptable de modo de proceso por lotes.

### <a name="adaptive-join-eligible-statements"></a>Instrucciones aptas de combinación adaptable
Algunas condiciones convierten a una combinación lógica en apta como combinación adaptable de modo de proceso por lotes:
- El nivel de compatibilidad de la base de datos es 140
- La consulta es una instrucción SELECT (las instrucciones de modificación de datos no son aptas actualmente)
- La combinación puede ser ejecutada tanto por una combinación de bucle anidado indizada como por un algoritmo físico de combinación hash
- La combinación hash usa el modo por lotes, ya sea mediante la presencia de un índice de almacén de columnas en la consulta global o una referencia directa a la tabla con índice de almacén de columnas por parte de la combinación
- Las soluciones alternativas generadas de la combinación de bucle anidado y la combinación hash deben tener el mismo primer elemento secundario (referencia externa)

### <a name="adaptive-joins-and-nested-loop-efficiency"></a>Combinaciones adaptables y eficacia del bucle anidado
Si una combinación adaptable cambia a una operación de bucle anidado, usa las filas ya leídas por la compilación de combinación hash. El operador *no* vuelve a leer las filas de la referencia externa.

### <a name="adaptive-threshold-rows"></a>Filas de umbral adaptable
El gráfico siguiente muestra una intersección de ejemplo entre el costo de una combinación hash y el de una alternativa de combinación de bucle anidado.  En este punto de intersección, se determina el umbral que a su vez determina el algoritmo real usado para la operación de combinación.

![Umbral de combinación](./media/6_AQPJoinThreshold.png)

## <a name="interleaved-execution-for-multi-statement-table-valued-functions"></a>Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones
La ejecución intercalada cambia el límite unidireccional entre las fases de optimización y ejecución de una ejecución de una sola consulta y permite que los planes se adapten en función de las estimaciones de cardinalidad revisadas. Durante la optimización, si se detecta un candidato para la ejecución intercalada, que son actualmente las **funciones con valores de tabla de múltiples instrucciones (MSTVF)**, se detiene la optimización, se ejecuta el subárbol aplicable, se capturan las estimaciones de cardinalidad precisas y luego se reanuda la optimización de las operaciones de nivel inferior.
Las MSTVF tienen una estimación de cardinalidad fija de "100" en SQL Server 2014 y SQL Server 2016 y de "1" en versiones anteriores. La ejecución intercalada ayuda con los problemas de rendimiento de cargas de trabajo debidos a estas estimaciones de cardinalidad fijas asociadas a las funciones con valores de tabla de múltiples instrucciones.

En la siguiente imagen se muestran los resultados estadísticos de una consulta activa, un subconjunto de un plan de ejecución global que refleja el impacto de las estimaciones de cardinalidad fijas de MSTVF. Puede ver el flujo de filas real frente a las filas estimadas. Hay tres áreas reseñables del plan (el flujo va de derecha a izquierda):
1. El recorrido de tabla de MSTVF tiene una estimación fija de 100 filas. Pero en este ejemplo hay *527.597* filas que pasan por este recorrido de tabla de MSTVF, como se muestra en las estadísticas de consultas activas a través de "527597 de 100" reales de estimados, por lo que la estimación fija está considerablemente desviada.
1. En el caso de la operación de bucles anidados, se supone que el lado externo de la combinación solo devuelve 100 filas. Dado el gran número de filas que las MSTVF devuelven en realidad, es probable que lo mejor sea un algoritmo de combinación totalmente diferente.
1. En el caso de la operación de coincidencia de hash, observe el pequeño símbolo de advertencia, que en este caso indica un desbordamiento en el disco.

![Flujo de filas frente a filas estimadas](./media/7_AQPFlowThreeAreas.png)

Compare el plan anterior con el plan real generado con la ejecución intercalada habilitada:

![Plan intercalado](./media/8_AQPInterleavedEnabledPlan.png)

1. Observe que el recorrido de tabla de MSTVF ahora refleja una estimación de cardinalidad precisa. Observe también la reordenación de este recorrido de tabla y las demás operaciones.
1. Con respecto a los algoritmos de combinación, se ha pasado de una operación de bucle anidado a una operación de coincidencia de hash, que es más adecuada dado el gran número de filas implicadas.
1. Observe también que ya no hay advertencias de desbordamiento, ya que se ha concedido más memoria en función del recuento real de filas que pasan desde el recorrido de tabla de MSTVF.

### <a name="interleaved-execution-eligible-statements"></a>Instrucciones aptas de ejecución intercalada
Las instrucciones que hacen referencia a las MSTVF en la ejecución intercalada de momento deben ser de solo lectura y no formar parte de ninguna operación de modificación de datos. Además, las MSTVF no serán aptas para la ejecución intercalada si se usan en el interior de una operación CROSS APPLY.

### <a name="interleaved-execution-benefits"></a>Ventajas de la ejecución intercalada
En general, cuanta mayor sea la distorsión entre el número de filas real y el estimado, además del número de operaciones de nivel inferior del plan, mayor será el impacto sobre el rendimiento.
En general, la ejecución intercalada beneficia a las consultas donde:
1. Hay una gran distorsión entre el número real de filas y el estimado del conjunto de resultados intermedio (en este caso, las MSTVF) y...
1. ... la consulta global es sensible a un cambio en el tamaño del resultado intermedio. Esto suele suceder cuando hay un árbol complejo por encima de ese subárbol en el plan de consulta.
Un simple "SELECT *" de una MSTVF no se beneficiará de la ejecución intercalada.

### <a name="interleaved-execution-overhead"></a>Sobrecarga de la ejecución intercalada
La sobrecarga debe ser de mínima a ninguna. Las MSTVF ya se estaban materializando antes de la introducción de la ejecución intercalada; la diferencia es que ahora se permite la optimización diferida y luego se aprovecha la estimación de cardinalidad del conjunto de filas materializado.
Al igual que cualquier plan que afecte a los cambios, algunos planes podrían cambiar de modo que con la mejor cardinalidad del subárbol se obtuviera un plan peor para la consulta en general. La mitigación puede incluir la reversión del nivel de compatibilidad o el uso del Almacén de consultas para aplicar la versión no revertida del plan.

### <a name="interleaved-execution-and-consecutive-executions"></a>Ejecución intercalada y ejecuciones consecutivas
Una vez que se almacena en caché un plan de ejecución intercalada, el plan con las estimaciones revisadas en la primera ejecución se usa para las ejecuciones consecutivas sin volver a crear una instancia de ejecución intercalada.

### <a name="tracking-interleaved-execution-activity"></a>Seguimiento de la actividad de ejecución intercalada
Puede ver los atributos de uso en el plan de ejecución de consulta real:

| Atributo de plan | Description |
| --- | --- |
| ContainsInterleavedExecutionCandidates | Si la aplicación al nodo *QueryPlan* es "true" significa que el plan contiene candidatos de ejecución intercalada. |
| IsInterleavedExecuted | El atributo está dentro del elemento RuntimeInformation bajo el elemento RelOp del nodo de TVF. Si es "true", significa que la operación se ha materializado como parte de una operación de ejecución intercalada. |

También puede realizar el seguimiento de repeticiones de ejecución intercalada mediante los siguientes eventos de XEvents:

| XEvent | Description |
| ---- | --- |
| interleaved_exec_status | Este evento se desencadena cuando se está produciendo la ejecución intercalada. |
| interleaved_exec_stats_update | Este evento describe las estimaciones de cardinalidad actualizadas por la ejecución intercalada. |
| Interleaved_exec_disabled_reason | Este evento se desencadena cuando una consulta con un posible candidato para la ejecución intercalada no consigue realmente la ejecución intercalada. |

Se debe ejecutar una consulta para permitir que la ejecución intercalada revise las estimaciones de cardinalidad de MSTVF. Pero el plan de ejecución estimado aún muestra cuándo hay candidatos de ejecución intercalada a través del atributo ContainsInterleavedExecutionCandidates.

### <a name="interleaved-execution-caching"></a>Almacenamiento en caché de la ejecución intercalada
Si un plan se borra o se elimina de la memoria caché, al ejecutarse la consulta se genera una nueva compilación que usa la ejecución intercalada.
Una instrucción con OPTION(RECOMPILE) creará un plan con ejecución intercalada y no lo almacenará en la memoria caché.

### <a name="interleaved-execution-and-query-store-interoperability"></a>Ejecución intercalada e interoperabilidad del Almacén de consultas
Los planes con ejecución intercalada se pueden aplicar. El plan es la versión que ha corregido las estimaciones de cardinalidad basándose en la ejecución inicial.

## <a name="see-also"></a>Vea también

[Centro de rendimiento para el motor de base de datos SQL Server y Azure SQL Database](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)

[Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md)

[Demostración del procesamiento de consultas adaptable](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)      


