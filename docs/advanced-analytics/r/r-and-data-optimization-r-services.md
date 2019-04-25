---
title: 'Optimización del rendimiento para la optimización de datos: SQL Server Machine Learning Services'
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4fdc699437ef44d32e944d810e9e38571d20472c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642277"
---
# <a name="performance-for-r-services---data-optimization"></a>Rendimiento de R Services: optimización de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo es el tercero de una serie que se describe la optimización del rendimiento para servicios de R según dos casos prácticos. Este artículo describen las optimizaciones del rendimiento de R o Python scripts que se ejecutan en SQL Server. También describe los métodos que puede usar para actualizar el código de R, para mejorar el rendimiento y evitar problemas conocidos.

## <a name="choosing-a-compute-context"></a>Elección de un contexto de proceso

En SQL Server 2016 y 2017, puede usar el **local** o **SQL** contexto de proceso cuando se ejecuta el script de R o Python.

Cuando se usa el **local** contexto de proceso de análisis se realiza en el equipo y no en el servidor. Por lo tanto, si está obteniendo datos de SQL Server para usar en el código, se deben buscar los datos a través de la red. El impacto en el rendimiento en el que se incurre para esta transferencia de red depende del tamaño de los datos transferidos, la velocidad de la red y otras transferencias de red que se producen al mismo tiempo.

Cuando se usa el **contexto de proceso de SQL Server**, el código se ejecuta en el servidor. Si está obteniendo datos de SQL Server, los datos deben ser locales en el servidor que ejecuta el análisis y, por lo tanto, no se introduce ninguna sobrecarga de la red. Si necesita importar datos desde otros orígenes, considere la posibilidad de organizar ETL con antelación.

Cuando se trabaja con grandes conjuntos de datos, se debe usar siempre el contexto de cálculo SQL.

## <a name="factors"></a>Factores

El lenguaje R tiene el concepto de *factores*, que son variables especiales para datos de categorías. Los científicos de datos a menudo usan variables de factor en sus fórmulas, dado que las variables de categorías como factores de control garantiza que los datos se procesó correctamente funciones de machine learning. Para obtener más información, consulte [R para Dummies: Variables de factor](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

Por diseño, variables de factor pueden convertirse de cadenas en enteros y vuelva a intentarlo para almacenarlos o procesarlos. R `data.frame` función controla todas las cadenas como variables de factor, a menos que el argumento *stringsAsFactors* está establecido en **False**. Esto significa si las cadenas tienen automáticamente se convierte en un entero para el procesamiento y, a continuación, asignar a la cadena original.

Si los datos de origen para factores se almacenan como un entero, rendimiento puede verse afectado, ya que R convierte a los enteros de factor en cadenas en tiempo de ejecución y, a continuación, realiza su propia conversión de cadena a entero interno.

Para evitar estas conversiones en tiempo de ejecución, considere la posibilidad de almacenar los valores como enteros en la tabla de SQL Server y utilizar el _colInfo_ argumento para especificar los niveles de la columna que se utiliza como factor. Objetos de origen de datos la mayoría de RevoScaleR toman el parámetro _colInfo_. Utilice este parámetro para nombrar las variables utilizadas por el origen de datos, especificar su tipo y definir los niveles de las variables o las transformaciones en los valores de columna.

Por ejemplo, la siguiente llamada de función de R obtiene los enteros 1, 2 y 3 de una tabla, pero asigna los valores en un factor con niveles "apple", "orange" y "banana".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Cuando la columna de origen contiene cadenas, siempre es más eficaz para especificar los niveles antes de tiempo mediante la _colInfo_ parámetro. Por ejemplo, el siguiente código R trata las cadenas como factores, como se leen.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Si no hay ninguna diferencia semántica en la generación del modelo, el último enfoque puede provocar un rendimiento mejor.

## <a name="data-transformations"></a>Transformaciones de datos

Los científicos de datos suelen emplear funciones de transformación escritas en R como parte del análisis. La función de transformación se aplica a cada fila que se recuperan de la tabla. En SQL Server, estas transformaciones se aplican a todas las filas recuperadas en un lote, lo que requiere comunicación entre el intérprete de R y el motor de análisis. Para realizar la transformación, se mueven los datos de SQL al motor de análisis y, después, al proceso del intérprete de R y viceversa.

Por este motivo, el uso de transformaciones como parte del código de R puede tener un importante efecto adverso en el rendimiento del algoritmo, según la cantidad de datos implicados.

Resulta más eficaz tener todas las columnas necesarias en la tabla o vista antes de realizar análisis y evitar las transformaciones durante el cálculo. Si no es posible agregar más columnas a las tablas existentes, considere la posibilidad de crear otra tabla o vista con las columnas transformadas y usar una consulta adecuada para recuperar los datos.

## <a name="batch-row-reads"></a>Lee la fila del lote

Si usa un origen de datos de SQL Server (`RxSqlServerData`) en el código, se recomienda que intente usar el parámetro _rowsPerRead_ para especificar el tamaño del lote. Este parámetro define el número de filas que se consultan y, a continuación, se envía a la secuencia de comandos externo para su procesamiento. En tiempo de ejecución, el algoritmo ve solo el número especificado de filas en cada lote.

La capacidad de controlar la cantidad de datos que se procesan a la vez puede ayudarle a resolver o evitar problemas. Por ejemplo, si el conjunto de datos de entrada es muy grande (tiene muchas columnas), o si el conjunto de datos tiene unas pocas columnas de gran tamaño (como texto sin formato), puede reducir el tamaño del lote para evitar la paginación de datos no hay memoria suficiente.

De forma predeterminada, el valor de este parámetro se establece en 50000, para garantizar un rendimiento aceptable incluso en equipos con poca memoria. Si el servidor tiene suficiente memoria disponible, al aumentar este valor a 500 000 o incluso un millón puede producir un mejor rendimiento, especialmente para las tablas grandes.

Las ventajas de aumentar el tamaño del lote eran evidente en un conjunto de datos grande y en una tarea que se puede ejecutar en varios procesos. Sin embargo, al aumentar este valor no siempre genera los mejores resultados. Se recomienda que experimente con los datos y el algoritmo para determinar el valor óptimo.

## <a name="parallel-processing"></a>procesamiento en paralelo

Para mejorar el rendimiento de **rx** funciones analíticas, puede aprovechar la capacidad de SQL Server para ejecutar tareas en paralelo mediante núcleos disponibles en el equipo del servidor.

Hay dos formas de lograr la ejecución en paralelo con R en SQL Server:

-   **Use \@paralelas.** Cuando se usa el procedimiento almacenado `sp_execute_external_script` para ejecutar un script de R, se establece el parámetro `@parallel` en `1`. Este es el mejor método si el script de R no **no** usar funciones de RevoScaleR, que tienen otros mecanismos para su procesamiento. Si su script usa funciones de RevoScaleR (generalmente tienen el prefijo "rx"), procesamiento en paralelo se realiza automáticamente y no es necesario establecer explícitamente `@parallel` a `1`.

    Si el script de R se puede ejecutar en paralelo, y se puede paralelizar la consulta SQL, el motor de base de datos crea varios procesos en paralelo. El número máximo de procesos que se pueden crear es igual a la **grado máximo de paralelismo** configuración (MAXDOP) para la instancia. Todos los procesos, a continuación, ejecución el mismo script, pero solo una parte de los datos de recepción.
    
    Por lo tanto, este método no es útil con scripts que deben ver todos los datos, como al entrenar un modelo. Pero resulta útil al realizar tareas como la predicción por lotes en paralelo. Para obtener más información sobre el uso de paralelismo con `sp_execute_external_script`, consulte el **sugerencias avanzada: procesamiento en paralelo** sección de [mediante código de R en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Usar numTasks = 1.** Cuando se usa **rx** funciones en un contexto de proceso de SQL Server, establezca el valor de la _numTasks_ parámetro para el número de procesos que le gustaría crear. El número de procesos creados nunca puede ser más de **MAXDOP**; sin embargo, se determina el número real de los procesos creados por el motor de base de datos y puede ser menor de lo que solicita.

    Si el script de R se puede ejecutar en paralelo, y se puede paralelizar la consulta SQL, SQL Server crea varios procesos en paralelo al ejecutar las funciones rx. El número real de los procesos que se crean depende de una variedad de factores como la regulación de recursos, el uso actual de los recursos, otras sesiones y el plan de ejecución de consulta para la consulta utilizada con el script de R.

## <a name="query-parallelization"></a>Paralelización de consultas

En Microsoft R, puede trabajar con orígenes de datos de SQL Server mediante la definición de los datos como un objeto de origen de datos RxSqlServerData.

Crea un origen de datos basado en una tabla o vista completa:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Crea un origen de datos basado en una consulta SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Si se especifica una tabla en el origen de datos en lugar de una consulta, R Services usa la heurística interna a determina las columnas necesarias para capturar de la tabla. Sin embargo, este enfoque es poco probable que resulta en ejecución en paralelo.

Para asegurarse de que se pueden analizar los datos en paralelo, la consulta utilizada para recuperar los datos debe configurarse de tal manera que el motor de base de datos puede crear un plan de consulta en paralelo. Si el código o el algoritmo utiliza grandes volúmenes de datos, asegúrese de que la consulta proporcionada a `RxSqlServerData` está optimizado para la ejecución en paralelo. Una consulta que no da como resultado un plan de ejecución en paralelo puede producir un único proceso para el cálculo.

Si necesita trabajar con grandes conjuntos de datos, use Management Studio o el otro analizador de consultas SQL antes de ejecutar el código de R para analizar el plan de ejecución. A continuación, tome las medidas recomendadas para mejorar el rendimiento de la consulta. Por ejemplo, un índice que falta en una tabla puede afectar al tiempo necesario para ejecutar una consulta. Para obtener más información, consulte [supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Otro error común que puede afectar al rendimiento es que una consulta recupera más columnas que son necesarios. Por ejemplo, si una fórmula se basa en sólo tres columnas, pero la tabla de origen tiene 30 columnas, va a mover datos innecesariamente.

 + Evite el uso de `SELECT *`!
 + Tardar algún tiempo para revisar las columnas del conjunto de datos e identificar sólo los que se necesitan para el análisis
 + Quite de las consultas de las columnas que contienen tipos de datos que no son compatibles con el código de R, tales como GUID y rowguid
 + Verificación de fecha no compatible y formatos de hora
 + En lugar de cargar una tabla, crear una vista que selecciona ciertos valores o convierte las columnas para evitar errores de conversión

## <a name="optimizing-the-machine-learning-algorithm"></a>Optimizar el algoritmo de aprendizaje automático

Esta sección proporcionan varias sugerencias y recursos que son específicos a RevoScaleR y otras opciones en Microsoft R.

> [!TIP]
> Una discusión general de la optimización de R está fuera del ámbito de este artículo. Sin embargo, si tiene que tomar el código más rápido, se recomienda el artículo popular, [The Inferno R](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Se tratan los errores habituales en lenguaje muy descriptivos y los detalles y construcciones de programación en R y proporciona muchos ejemplos específicos de las técnicas de programación R.

### <a name="optimizations-for-revoscaler"></a>Optimizaciones de RevoScaleR

Muchos algoritmos RevoScaleR admiten parámetros para controlar cómo se genera el modelo entrenado. Aunque la precisión y la exactitud del modelo es importante, el rendimiento del algoritmo podría ser igualmente importante. Para obtener un equilibrio entre la precisión y tiempo de entrenamiento, puede modificar los parámetros para aumentar la velocidad de cálculo y, en muchos casos, mejorar el rendimiento sin reducir la precisión o exactitud.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` admite la `maxDepth` parámetro, que controla la profundidad del árbol de decisión. Como `maxDepth` es aumenta, el rendimiento puede disminuir, por lo que es importante analizar las ventajas de aumentar la profundidad frente afecta negativamente al rendimiento.

    También puede controlar el equilibrio entre la precisión de complejidad y la predicción del tiempo mediante el ajuste de parámetros como `maxNumBins`, `maxDepth`, `maxComplete`, y `maxSurrogate`. Aumentar la profundidad por encima de 10 o 15 puede hacer que el cálculo sea muy costoso.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Pruebe a usar el `cube` argumento si la primera variable dependiente en la fórmula es una variable de factor.
    
    Cuando `cube` está establecido en `TRUE`, la regresión se realiza mediante un inverso con particiones, que podría ser más rápido y utiliza menos memoria que el cálculo de regresión estándar. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser significativa.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Use el `cube` argumento si la primera variable dependiente es una variable de factor.
    
    Cuando `cube` está establecido en `TRUE`, el algoritmo utiliza un inverso con particiones, lo que podría ser más rápido y utiliza menos memoria. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser significativa.

Para obtener orientación adicional sobre la optimización de RevoScaleR, consulte estos artículos:

+ Artículo de soporte técnico: [Opciones de rxdforest/rxDTree de optimización del rendimiento](https://support.microsoft.com/kb/3104235)

+ Métodos para controlar el modelo que caben en un modelo de árbol ampliado: [Estimación de los modelos de uso de potenciación del gradiente estocástico](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Información general de cómo se mueve y procesa datos RevoScaleR: [Escribir algoritmos personalizados de fragmentación de ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modelo de programación para RevoScaleR: [Administración de subprocesos de RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Referencia de función para [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Referencia de función para [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Use MicrosoftML

También recomendamos que observa en el nuevo **MicrosoftML** paquete, que proporciona los algoritmos de aprendizaje automático escalable que pueden usar los contextos de cálculo y transformaciones de RevoScaleR.

+ [Introducción a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Cómo elegir un algoritmo de MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Hacer operativa una solución con Microsoft R Server

Si su escenario implica la predicción rápida mediante un modelo almacenado o la integración de aprendizaje automático en una aplicación, puede usar el [operacionalización](https://docs.microsoft.com/r-server/what-is-operationalization) características de Microsoft R Server (anteriormente conocidas como DeployR).

+ Como un **científico de datos**, utilice el [paquete mrsdeploy](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) para compartir código de R con otros equipos e integrar análisis de R en aplicaciones web, escritorio, móviles y panel: [Cómo publicar y administrar servicios web de R en R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Como un **administrador**, obtenga información sobre cómo administrar paquetes, supervisar nodos de web y nodos de proceso y controlar la seguridad de los trabajos de R: [Cómo interactúan y consumir servicios web en R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Performance tuning para R - Introducción](sql-server-r-services-performance-tuning.md)

[Optimización del rendimiento de R - configuración de SQL Server](sql-server-configuration-r-services.md)

[Optimización del rendimiento de R: R optimización de código y los datos](r-and-data-optimization-r-services.md)

[Los resultados del caso práctico: optimización del rendimiento](performance-case-study-r-services.md)
