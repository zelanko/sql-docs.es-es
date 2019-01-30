---
title: Procesamiento de consultas inteligente en bases de datos de Microsoft SQL | Microsoft Docs
description: Características de procesamiento de consultas inteligente para mejorar el rendimiento de las consultas en SQL Server y Azure SQL Database.
ms.custom: ''
ms.date: 01/11/2019
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
ms.openlocfilehash: e07bfa316330a24e9a7b9db5a2486ddd7cad470c
ms.sourcegitcommit: b51edbe07a0a2fdb5f74b5874771042400baf919
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2019
ms.locfileid: "55087805"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Procesamiento de consultas inteligente en bases de datos SQL

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La familia de características de **procesamiento de consultas inteligente** incluye características con un gran impacto que mejoran el rendimiento de las cargas de trabajo existentes con un esfuerzo de implementación mínimo.  Puede beneficiarse automáticamente de esta familia de características si migra al nivel de compatibilidad de base de datos aplicable.

![Características de procesamiento de consultas inteligentes](./media/3_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>Procesamiento de consultas adaptable

La familia de características de procesamiento de consultas adaptable incluye mejoras en el procesamiento de consultas que adaptan las estrategias de optimización a las condiciones de tiempo de ejecución de la carga de trabajo de la aplicación. Estas mejoras incluyen: 
- Combinaciones adaptables de modo de proceso por lotes
- Comentarios de concesión de memoria
- Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones (MSTVF)

### <a name="batch-mode-adaptive-joins"></a>Combinaciones adaptables de modo de proceso por lotes

Esta característica permite cambiar su plan de forma dinámica a una mejor estrategia de combinación durante la ejecución mediante un único plan almacenado en caché.

Para obtener más información sobre las combinaciones adaptables de modo de proceso por lotes, vea [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Comentarios de concesión de memoria del modo de fila y el modo de proceso por lotes

> [!NOTE]
> Los comentarios de concesión de memoria del modo de fila es una característica en vista previa (GB) pública.  

Esta característica recalcula la memoria real necesaria para una consulta y actualiza el valor de la concesión del plan almacenado en caché, con lo que se reducen las concesiones de memoria excesivas que afectan a la simultaneidad y se corrigen concesiones de memoria subestimadas que provocan desbordamientos costosos en el disco.

Para obtener más información sobre los comentarios de concesión de memoria, vea [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>Ejecución intercalada de funciones con valores de tabla de múltiples instrucciones (MSTVF)

Con la ejecución intercalada se usan los recuentos de filas reales de la función para tomar decisiones fundamentadas sobre los planes de consulta descendentes. Para obtener más información sobre las funciones con valores de tabla de múltiples instrucciones, vea [ Funciones con valores de tabla](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

Para obtener más información sobre la ejecución intercalada, vea [Procesamiento de consultas adaptable en bases de datos SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilación diferida de variables de tabla

> [!NOTE]
> La compilación diferida de variables de tabla es una característica en vista previa pública.  

La compilación diferida de variables de tabla mejora la calidad del plan y el rendimiento general de las consultas que hacen referencia a las variables de tabla. Durante la optimización y la compilación inicial, esta característica propagará las estimaciones de cardinalidad que se basan en los recuentos de filas de variables de tabla reales.  Con la compilación diferida de variables de tabla, la compilación de una instrucción que hace referencia a una variable de tabla se difiere hasta la primera ejecución real de la instrucción.

Con la compilación aplazada variable de tabla, la compilación de una instrucción que hace referencia a una variable de tabla se aplaza hasta que la primera ejecución real de la instrucción. El comportamiento de esta compilación diferida es idéntico al comportamiento de las tablas temporales y este cambio genera el uso de la cardinalidad real en lugar de la estimación de una fila original. Para habilitar la versión preliminar pública de la compilación diferida de variables de tabla en Azure SQL Database, habilite el nivel 150 de compatibilidad de la base de datos para la base de datos a la que se conecta cuando ejecuta la consulta.

Para obtener más información, consulte [Compilación diferida de variables de tabla](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="scalar-udf-inlining"></a>Inserción de UDF escalar

> [!NOTE]
> Inserción de UDF escalar es una característica de versión preliminar pública.  

La inserción de UDF escalar transforma automáticamente [funciones definidas por el usuario (UDF) escalares](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) en expresiones relacionales y las inserta en la consulta SQL de llamada, lo que mejora el rendimiento de las cargas de trabajo que aprovechan las UDF escalares. La inserción de UDF escalar facilita la optimización basada en costos de las operaciones dentro de las UDF, y da como resultado planes eficaces paralelos y orientados a conjuntos en lugar de planes de ejecución ineficaces, iterativos y en serie. Esta característica está habilitada de forma predeterminada en el nivel de compatibilidad de base de datos 150.

Para obtener más información, vea [Scalar UDF inlining](../user-defined-functions/scalar-udf-inlining.md) (Inserción de UDF escalar).

## <a name="approximate-query-processing"></a>Procesamiento de consultas aproximado

> [!NOTE]
> APPROX_COUNT_DISTINCT es una característica en versión preliminar pública.  

El procesamiento de consultas aproximado es una nueva familia de características diseñadas para proporcionar agregaciones de conjuntos de datos de gran tamaño en los que la capacidad de respuesta resulta más fundamental que la precisión absoluta.  Un ejemplo podría ser calcular el valor COUNT(DISTINCT()) entre 10 mil millones de filas para mostrar en un panel.  En este caso, la precisión absoluta no es importante, pero la capacidad de respuesta es fundamental. La función de agregado APPROX_COUNT_DISTINCT nueva devuelve el número aproximado de valores no nulos únicos de un grupo.

Para más información, consulte [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modo de proceso por lotes en el almacén de filas 

> [!NOTE]
> El modo de proceso por lotes en el almacén de filas es una característica en vista previa pública.  

### <a name="background"></a>Información previa

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] introdujo una nueva característica para acelerar las cargas de trabajo de análisis: los índices de almacén de columnas. Hemos ampliado los casos de uso y mejorado el rendimiento de los índices de almacén de columnas en las versiones posteriores. Hasta ahora, se han descubierto y documentado todas estas funciones como una sola característica: se crean índices de almacén de columnas en las tablas y la carga de trabajo analítica "simplemente es más rápida". En segundo plano, sin embargo, hay dos conjuntos diferentes de tecnologías, aunque guardan relación:
- Los índices de **almacén de columnas** permiten a las consultas analíticas tener acceso solo a los datos de las columnas que necesitan. El formato de almacén de columnas también hace posible una compresión mucho más eficaz que la que se obtiene con la compresión de página en los índices de "almacén de filas" tradicionales. 
- El proceso en **modo por lotes** permite a los operadores de consulta procesar los datos más eficazmente al trabajar con todo un lote de filas a la vez, en lugar de con las filas de una en una. Hay más mejoras de escalabilidad relacionadas con el proceso en modo por lotes. Para obtener más información sobre el modo por lotes, vea [Modos de ejecución](../../relational-databases/query-processing-architecture-guide.md#execution-modes).

Los dos conjuntos de características funcionan conjuntamente para mejorar la utilización de E/S y CPU:
- Gracias a los índices de almacén de columnas caben más datos en la memoria y, por tanto, se requiere menos E/S.
- El proceso en modo por lotes utiliza la CPU de manera más eficaz.

Las dos tecnologías se apoyan entre sí siempre que es posible. Por ejemplo, es posible evaluar agregados del modo por lotes como parte de una exploración del índice de almacén de columnas. También se procesan los datos de un almacén de columnas comprimidos con codificación run-length de forma mucho más eficiente con combinaciones del modo por lotes y los agregados de modo por lotes. 
 
Las dos características ya se pueden utilizar por separado: puede obtener planes en modo de filas que utilizan índices de almacén de columnas, y puede obtener planes en modo por lotes que usan solo índices de almacén de filas. Pero puesto que en la mayoría de los casos obtiene mejores resultados cuando las dos características se usan juntas, el optimizador de consultas de SQL hasta ahora ha considerado el proceso en modo por lotes solo para las consultas que implican al menos una tabla con índice de almacén de columnas.

Para algunas aplicaciones, los índices de almacén de columnas no son una opción viable porque la aplicación usa alguna otra característica que no es compatible con los índices de almacén de columnas (no se admiten desencadenadores en tablas con índices de almacén de columnas agrupados, por ejemplo). Más importante aún, los índices de almacén de columnas agregan una sobrecarga para las instrucciones DELETE y UPDATE, porque las modificaciones en contexto no son compatibles con la compresión de almacén de columnas. Para algunas cargas de trabajo híbridas transaccionales y analíticas, la ventaja que aportan los índices de almacén de columnas a las consultas analíticas es superior que la sobrecarga que añaden a los aspectos transaccionales de una carga de trabajo. En tales escenarios puede obtener una mejor utilización de la CPU solo con el proceso en modo por lotes, por lo que la característica de **modo por lotes en el almacén de filas** considerará el modo por lotes para todas las consultas, independientemente de los índices implicados.

### <a name="what-workloads-may-benefit-from-batch-mode-on-rowstore"></a>¿Qué cargas de trabajo pueden beneficiarse del modo de proceso por lotes en el almacén de filas?

Las siguientes cargas de trabajo pueden beneficiarse del modo de proceso por lotes en el almacén de filas:
1. Una parte significativa de la carga de trabajo consiste en consultas analíticas (como regla general, las consultas con operadores, como combinaciones o agregados que procesan cientos de miles de filas o más), **Y**
2. La carga de trabajo depende de la CPU (si el cuello de botella es E/S, se sigue recomendando la posibilidad de considerar un índice de almacén de columnas, si es posible), **Y**
3. La creación de un índice de almacén de columnas agrega demasiada sobrecarga a la parte transaccional de la carga de trabajo **O** la creación de un índice de almacén de columnas no es viable porque la aplicación depende de una característica que no es compatible aún con los índices de almacén de columnas.

> [!NOTE]
> El modo de proceso por lotes en el almacén de filas solo sirve para reducir el consumo de CPU. Si el cuello de botella está relacionado con la E/S y los datos ya no están almacenados en caché (caché "en frío"), el modo de proceso por lotes en el almacén de filas NO mejorará el tiempo transcurrido. De forma similar, si no hay suficiente memoria en el equipo para almacenar en caché todos los datos, es poco probable que mejore el rendimiento.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>¿Qué cambios se producirán con el modo de proceso por lotes en el almacén de filas?

Aparte de pasar al nivel de compatibilidad 150, no es necesario que haga cambios para habilitar el modo de proceso por lotes en el almacén de filas para las cargas de trabajo candidatas.

Incluso si una consulta no implica ninguna tabla con un índice de almacén de columnas, el procesador de consultas ahora usa la heurística para decidir si se va a considerar el modo de proceso por lotes. La heurística consiste en:
1. Una comprobación inicial de tamaños de tablas, operadores utilizados y cardinalidades estimadas en la consulta de entrada.
2. Puntos de control adicionales, a medida que el optimizador detecta planes nuevos y más baratos para la consulta. Si estos planes alternativos no hacen un uso considerable del modo de proceso por lotes, el optimizador dejará explorar alternativas al modo por lotes.

Si se usa el modo de proceso por lotes en el almacén de filas, en el plan de ejecución de la consulta verá el modo de ejecución real como el “modo por lotes” utilizado por el operador de exploración para montones en disco e índices de árbol B.  Esta exploración del modo por lotes puede evaluar los filtros de mapa de bits del modo por lotes.  También es posible que vea otros operadores de modo por lotes en el plan, como las combinaciones hash, los agregados basados en hash, ordenaciones, agregados de ventana, filtros, concatenaciones y operadores Compute Scalar.

### <a name="remarks"></a>Notas

1. No existe ninguna garantía de que los planes de consulta usen el modo por lotes. El optimizador de consultas puede decidir que el modo por lotes no es beneficioso para la consulta. 
2. Como está cambiando el espacio de búsqueda del optimizador de consultas, no hay ninguna garantía de que si se obtiene un plan de modo de filas, este será el mismo que el plan que se obtenga en un nivel de compatibilidad inferior. Tampoco hay ninguna garantía de que si se obtiene un plan de modo por lotes, este será el mismo que el plan que se obtenga con un índice de almacén de columnas. 
3. Los planes también pueden cambiar de manera sutil para las consultas que combinan los índices de almacén de columnas y de almacén de filas como consecuencia de una nueva exploración del almacén de filas en modo por lotes.
4. Limitaciones actuales para el nuevo examen de modo por lotes en el almacén de filas: no se iniciará para tablas OLTP en memoria, ni para los índices que no sean de montones en disco y árboles B. Tampoco se iniciará si se captura o se filtra una columna LOB. Esta limitación incluye conjuntos de columnas dispersas y columnas XML.
5. Hay consultas para las que no se usa el modo por lotes ni siquiera con los índices de almacén de columnas (por ejemplo consultas que implican los cursores), y estas mismas exclusiones se aplican también al modo de proceso por lotes en el almacén de filas.

### <a name="configuring-batch-mode-on-rowstore"></a>Configuración del modo de proceso por lotes en el almacén de filas

La configuración de la base de datos de ámbito BATCH_MODE_ON_ROWSTORE está activada de forma predeterminada y puede usarse para deshabilitar el modo por lotes en el almacén de filas sin necesidad de un cambio en el nivel de compatibilidad de base de datos:

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

Puede deshabilitar el modo por lotes en el almacén de filas a través de la configuración de ámbito de base de datos, pero seguirá invalidando la configuración en el nivel de consulta mediante la sugerencia de consulta ALLOW_BATCH_MODE. El ejemplo siguiente habilita el modo por lotes en el almacén de filas incluso con la característica deshabilitada a través de la configuración de ámbito de base de datos:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

También puede deshabilitar el modo por lotes en el almacén de filas para una consulta específica mediante el uso de la sugerencia de consulta DISALLOW_BATCH_MODE. Por ejemplo:

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
[Query Processing Architecture Guide](../../relational-databases/query-processing-architecture-guide.md)   (Guía de arquitectura de procesamiento de consultas)  
[Referencia de operadores lógicos y físicos del plan de presentación](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Combinaciones](../../relational-databases/performance/joins.md)    
[Demostración del procesamiento de consultas adaptable](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[Demonstrating Intelligent QP](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md) (Demostración de QP inteligente)   
