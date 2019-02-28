---
title: Procesamiento de consultas inteligente en bases de datos de Microsoft SQL | Microsoft Docs
description: Características de procesamiento de consultas inteligente para mejorar el rendimiento de las consultas en SQL Server y Azure SQL Database.
ms.custom: ''
ms.date: 02/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dc47ad30edc0eb4092aa1f92fef703c95cb34593
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291663"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Procesamiento de consultas inteligente en bases de datos SQL

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La familia de características de procesamiento de consultas (QP) inteligentes incluye características con gran impacto. Mejoran el rendimiento de las cargas de trabajo existentes con un esfuerzo de implementación mínimo. Para beneficiarse automáticamente de esta familia de características, migre al nivel de compatibilidad de base de datos aplicable.

| **Característica de procesamiento de consultas inteligentes** | **Compatible con Azure SQL Database** | **Compatible con SQL Server** |
| --- | --- | --- |
| [Combinaciones adaptables (modo por lotes)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | Sí, en el nivel de compatibilidad 140| Sí, a partir de SQL Server 2017 en el nivel de compatibilidad 140|
| [Ejecución intercalada](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#interleaved-execution-for-multi-statement-table-valued-functions) | Sí, en el nivel de compatibilidad 140| Sí, a partir de SQL Server 2017 en el nivel de compatibilidad 140|
| [Comentarios de concesión de memoria (modo por lotes)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | Sí, en el nivel de compatibilidad 140| Sí, a partir de SQL Server 2017 en el nivel de compatibilidad 140|
| [Comentarios de concesión de memoria (modo de fila)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | Sí, en el nivel de compatibilidad 150, versión preliminar pública| Sí, a partir de SQL Server 2019 CTP 2.0 en el nivel de compatibilidad 150, versión preliminar pública|
| [Count Distinct aproximada](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | Sí, versión preliminar pública| Sí, a partir de SQL Server 2019 CTP 2.0, versión preliminar pública|
| [Compilación diferida de variables de tabla](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | Sí, en el nivel de compatibilidad 150, versión preliminar pública| Sí, a partir de SQL Server 2019 CTP 2.0 en el nivel de compatibilidad 150, versión preliminar pública|
| [Modo por lotes en el almacén de filas](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | Sí, en el nivel de compatibilidad 150, versión preliminar pública| Sí, a partir de SQL Server 2019 CTP 2.0 en el nivel de compatibilidad 150, versión preliminar pública|
| [Inserción de UDF escalar](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | No, pero se prevé para una actualización futura | Sí, a partir de SQL Server 2019 CTP 2.1 en el nivel de compatibilidad 150, versión preliminar pública|


## <a name="adaptive-query-processing"></a>Procesamiento de consultas adaptable

En la familia de características de procesamiento de consultas adaptable se incluyen las siguientes mejoras de procesamiento de consultas. Estas mejoras adaptan las estrategias de optimización a las condiciones de tiempo de ejecución de la carga de trabajo de la aplicación: 
- Combinaciones adaptables de modo de proceso por lotes
- Comentarios de concesión de memoria
- Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones (MSTVF)

### <a name="batch-mode-adaptive-joins"></a>Combinaciones adaptables de modo de proceso por lotes

Con esta característica, su plan puede cambiar de forma dinámica a una mejor estrategia de combinación durante la ejecución mediante un único plan almacenado en caché.

Para obtener más información sobre las combinaciones adaptables de modo de proceso por lotes, vea [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Comentarios de concesión de memoria del modo de fila y el modo de proceso por lotes

> [!NOTE]
> Los comentarios de concesión de memoria del modo de fila es una característica en vista previa (GB) pública.  

Esta característica recalcula la memoria real necesaria para una consulta. A continuación, actualiza el valor de concesión del plan en caché. Reduce las concesiones de memoria excesivas que afectan a la simultaneidad. Esta característica también soluciona las concesiones de memoria subestimadas que provocan costosos desbordamientos en disco.

Para obtener más información sobre los comentarios de concesión de memoria, vea [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="interleaved-execution-for-mstvfs"></a>Ejecución intercalada de MSTVF

Con la ejecución intercalada se usan los recuentos de filas reales de la función para tomar decisiones fundamentadas sobre los planes de consulta descendentes. Para obtener más información sobre las funciones con valores de tabla de múltiples instrucciones (MSTVF), consulte [ Funciones con valores de tabla](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

Para obtener más información sobre la ejecución intercalada, vea [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilación diferida de variables de tabla

> [!NOTE]
> La compilación diferida de variables de tabla es una característica en vista previa pública.  

La compilación diferida de variables de tabla mejora la calidad del plan y el rendimiento general de las consultas que hacen referencia a las variables de tabla. Durante la optimización y la compilación inicial, esta característica propaga las estimaciones de cardinalidad que se basan en los recuentos de filas de variables de tabla reales. Esta información precisa del recuento de filas optimiza las operaciones del plan de bajada.

La compilación diferida de variables de tabla aplaza la compilación de una instrucción que hace referencia a una variable de tabla hasta la primera ejecución real de la instrucción. Este comportamiento de compilación diferida es el mismo que el de las tablas temporales. Este cambio se traduce en el uso de la cardinalidad real en lugar de la estimación de una fila original. 

Puede habilitar la versión preliminar pública de la compilación diferida de variables de tabla en Azure SQL Database. Para ello, habilite el nivel de compatibilidad 150 para la base de datos a la que se conecta al ejecutar la consulta.

Para obtener más información, consulte [Compilación diferida de variables de tabla](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation).

## <a name="scalar-udf-inlining"></a>Inserción de UDF escalar

> [!NOTE]
> La inserción de la función definida por el usuario (UDF) escalar es una característica en versión preliminar pública.  

La inserción de UDF escalar transforma automáticamente las [UDF escalares](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) en expresiones relacionales. Las inserta en la consulta SQL de llamada. Esta transformación mejora el rendimiento de las cargas de trabajo que aprovechan las UDF escalares. La inserción de UDF escalar facilita la optimización basada en costos de las operaciones dentro de las UDF. Los resultados son eficaces, orientados a conjuntos y paralelos en lugar de tratarse de planes de ejecución seriales, iterativos e ineficaces. Esta característica está habilitada de forma predeterminada en el nivel de compatibilidad de base de datos 150.

Para obtener más información, vea [Inserción de UDF escalares](../user-defined-functions/scalar-udf-inlining.md).

## <a name="approximate-query-processing"></a>Procesamiento de consultas aproximado

> [!NOTE]
> **APPROX_COUNT_DISTINCT** es una característica en versión preliminar pública.  

El procesamiento de consultas aproximado es una nueva familia de características. Agrega conjuntos de datos de gran tamaño en los que la capacidad de respuesta resulta más fundamental que la precisión absoluta. Un ejemplo es calcular el valor **COUNT(DISTINCT())** entre 10 mil millones de filas para mostrar en un panel. En este caso, la precisión absoluta no es importante, pero la capacidad de respuesta es fundamental. La función de agregado **APPROX_COUNT_DISTINCT** nueva devuelve el número aproximado de valores no nulos únicos de un grupo.

Para más información, consulte [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modo por lotes en el almacén de filas 

> [!NOTE]
> El modo por lotes en el almacén de filas es una característica en versión preliminar pública.  

### <a name="background"></a>Información previa

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] introdujo una nueva característica para acelerar las cargas de trabajo de análisis: los índices de almacén de columnas. Ampliamos los casos de uso y mejoramos el rendimiento de los índices de almacén de columnas en las versiones posteriores. Hasta ahora, se han descubierto y documentado todas estas funciones como una sola característica. Crea los índices de almacén de columnas en sus tablas. Y su carga de trabajo de análisis va más rápido. Sin embargo, hay dos conjuntos diferentes de tecnologías, aunque guardan relación:
- Con los índices de **almacén de columnas**, las consultas analíticas tienen acceso solo a los datos de las columnas que necesitan. La compresión de página en formato de almacén de columnas también es más eficaz que la compresión en los índices de **almacén de filas** tradicionales. 
- Con el procesamiento de **modo por lotes**, los operadores de consulta procesan los datos con mayor eficacia. Funcionan en un lote de filas en lugar de una fila cada vez. Hay más mejoras de escalabilidad relacionadas con el proceso en modo por lotes. Para obtener más información sobre el modo por lotes, consulte [Modos de ejecución](../../relational-databases/query-processing-architecture-guide.md#execution-modes).

Los dos conjuntos de características funcionan conjuntamente para mejorar la utilización de entrada/salida (E/S) y CPU:
- Mediante el uso de índices de almacén de columnas, más datos suyos caben en la memoria. Eso reduce la necesidad de E/S.
- El proceso en modo por lotes utiliza la CPU de manera más eficaz.

Las dos tecnologías se apoyan entre sí siempre que es posible. Por ejemplo, es posible evaluar agregados del modo por lotes como parte de una exploración del índice de almacén de columnas. También se procesan los datos de un almacén de columnas comprimidos con codificación run-length de forma mucho más eficiente con combinaciones del modo por lotes y los agregados de modo por lotes. 
 
Las dos características se pueden usar de forma independiente:
* Obtiene planes de modo de fila que usan índices de almacén de columnas.
* Obtiene planes de modo por lotes que usan índices de almacén de filas. 

Normalmente obtiene los mejores resultados al usar las dos características conjuntamente. Así pues, hasta ahora, el optimizador de consultas de SQL Server ha tenido en cuenta el procesamiento de modo por lotes solo para aquellas consultas que implican al menos una tabla con un índice de almacén de columnas.

Los índices de almacén de columnas no son una buena opción para algunas aplicaciones. Una aplicación podría usar cualquier otra característica no compatible con los índices de almacén de columnas. Por ejemplo, las modificaciones en contexto no son compatibles con la compresión del almacén de columnas. De este modo, los desencadenadores no se admiten en tablas con índices de almacén de columnas en clúster. Y, lo que es más importante, los índices de almacén de columnas agregan sobrecarga para las instrucciones **DELETE** y **UPDATE**. 

Para algunas cargas de trabajo híbridas transaccionales y analíticas, la sobrecarga que añaden a los aspectos transaccionales de una carga de trabajo es superior que las ventajas de los índices de almacén de columnas. Estos escenarios pueden mejorar el uso de CPU desde el procesamiento de modo por lotes solamente. Por eso, el modo por lotes en la característica de almacén de filas tiene en cuenta el modo por lotes para todas las consultas. No importa qué índices están implicados.

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>Cargas de trabajo que pueden beneficiarse del modo por lotes en el almacén de filas

Las siguientes cargas de trabajo pueden beneficiarse del modo por lotes en el almacén de filas:
* una parte significativa de la carga de trabajo consta de consultas analíticas. Normalmente, estas consultas tienen operadores como combinaciones o agregados que procesan cientos de miles de filas o más.
* La carga de trabajo está enlazada a la CPU. Si el cuello de botella es E/S, seguimos recomendando que tenga en cuenta un índice de almacén de columnas, si es posible.
* La creación de un índice de almacén de columnas agrega demasiada sobrecarga al elemento transaccional de su carga de trabajo. O bien, la creación de un índice de almacén de columnas no sería factible porque la aplicación depende de una característica que no es compatible aún con los índices de almacén de columnas.

> [!NOTE]
> El modo por lotes en el almacén de filas solo sirve para reducir el consumo de CPU. Si el cuello de botella está relacionado con la E/S y los datos ya no están almacenados en caché (caché "en frío"), el modo por lotes en el almacén de filas no mejorará el tiempo transcurrido. De forma similar, si no hay suficiente memoria en el equipo para almacenar en caché todos los datos, es poco probable que mejore el rendimiento.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>¿Qué cambios se producirán con el modo por lotes en el almacén de filas?

Aparte de pasar al nivel de compatibilidad 150, no es necesario que haga cambios para habilitar el modo por lotes en el almacén de filas para las cargas de trabajo candidatas.

Incluso si una consulta no implica ninguna tabla con un índice de almacén de columnas, el procesador de consultas ahora usa la heurística para decidir si se va a tener en cuenta el modo por lotes. La heurística consiste en estas comprobaciones:
1. Una comprobación inicial de tamaños de tablas, operadores utilizados y cardinalidades estimadas en la consulta de entrada.
2. Puntos de control adicionales, a medida que el optimizador detecta planes nuevos y más baratos para la consulta. Si estos planes alternativos no hacen un uso considerable del modo por lotes, el optimizador dejará explorar alternativas al modo por lotes.

Si se usa el modo por lotes en el almacén de filas, verá el modo de ejecución real como **modo por lotes** en el plan de consulta. El operador de examen usa el modo por lotes para montones en disco e índices de árbol B. Esta exploración del modo por lotes puede evaluar los filtros de mapa de bits del modo por lotes. También podría ver otros operadores del modo por lotes en el plan. Entre los ejemplos se incluyen combinaciones hash, agregados basados en hash, ordenaciones, agregados de ventana, filtros, concatenación y operadores Compute Scalar.

### <a name="remarks"></a>Notas

* Los planes de consulta no siempre usan el modo por lotes. El optimizador de consultas puede decidir que el modo por lotes no es beneficioso para la consulta. 
* El espacio de búsqueda del optimizador de consultas está cambiando. Así pues, si obtiene un plan de modo de fila, podría no ser igual al plan obtenido en un nivel de compatibilidad más bajo. Y, si obtiene un plan de modo por lotes, podría no ser igual al plan obtenido con un índice de almacén de columnas. 
* Los planes también pueden cambiar para las consultas que combinan los índices de almacén de columnas y de almacén de filas como consecuencia de una nueva exploración del almacén de filas en modo por lotes.
* Existen limitaciones actuales para el nuevo examen de modo por lotes en el almacén de filas: 
    * no se iniciará para tablas OLTP en memoria, ni para los índices que no sean de montones en disco y árboles B. 
    * Tampoco se iniciará si se captura o se filtra una columna de objetos de gran tamaño (LOB). Esta limitación incluye conjuntos de columnas dispersas y columnas XML.
* Hay consultas para las que no se usa el modo por lotes incluso con índices de almacén de columnas. Entre los ejemplos se incluyen consultas que implican cursores. Estas mismas exclusiones también se amplían al modo por lotes en el almacén de filas.

### <a name="configure-batch-mode-on-rowstore"></a>Configuración del modo por lotes en el almacén de filas

La configuración de ámbito de base de datos **BATCH_MODE_ON_ROWSTORE** está activada de forma predeterminada. Deshabilita el modo por lotes en el almacén de filas sin necesidad de un cambio en el nivel de compatibilidad de la base de datos:

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

puede deshabilitar el modo por lotes en el almacén de filas a través de la configuración de ámbito de base de datos. Pero aún puede invalidar la configuración en el nivel de consulta con la sugerencia de consulta **ALLOW_BATCH_MODE**. El ejemplo siguiente habilita el modo por lotes en el almacén de filas incluso con la característica deshabilitada a través de la configuración de ámbito de base de datos:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

También puede deshabilitar el modo por lotes en el almacén de filas para una consulta específica mediante el uso de la sugerencia de consulta **DISALLOW_BATCH_MODE**. Vea el ejemplo siguiente:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>Vea también

[Performance Center for SQL Server Database Engine and Azure SQL Database](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)    (Centro de rendimiento para el motor de base de datos SQL Server y Azure SQL Database)  
[Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Combinaciones](../../relational-databases/performance/joins.md)    
[Demostración del procesamiento de consultas adaptable](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[Demonstrating Intelligent QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md) (Demostración de QP inteligente)   
