---
title: "Rendimiento de los servicios de R - optimización datos | Documentos de Microsoft"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df91cedac15da65bee9c9aa38c3c747e04f6d60d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="performance-for-r-services---data-optimization"></a>Rendimiento de R Services: optimización de datos

En este artículo es el tercero de una serie que describe la optimización de rendimiento para servicios de R que se basa en dos casos prácticos. En este artículo se describe las optimizaciones de rendimiento para R o Python scripts que se ejecutan en SQL Server. También se describen los métodos que puede usar para actualizar el código de R, para mejorar el rendimiento y evitar problemas conocidos.

## <a name="choosing-a-compute-context"></a>Elegir un contexto de proceso

En SQL Server 2016 y de 2017, puede usar el **local** o **SQL** contexto de proceso cuando se ejecuta el script de R o Python.

Cuando se usa el **local** contexto de proceso de análisis se realiza en el equipo y no en el servidor. Por lo tanto, si está obteniendo datos de SQL Server para usar en el código, se deben recopilar los datos a través de la red. El impacto en el rendimiento en el que se incurre para esta transferencia de red depende del tamaño de los datos transferidos, la velocidad de la red y otras transferencias de red que se producen al mismo tiempo.

Cuando se usa el **contexto de proceso de SQL Server**, el código se ejecuta en el servidor. Si va a obtener datos de SQL Server, deben ser locales al servidor que ejecuta el análisis de los datos y, por tanto, no se introduce ninguna sobrecarga de la red. Si necesita importar datos desde otros orígenes, considere la posibilidad de organizar ETL de antemano.

Cuando se trabaja con grandes conjuntos de datos, se debe usar siempre el contexto de cálculo SQL.

## <a name="factors"></a>Factores

El lenguaje R tiene el concepto de "factores", que son variables especiales para datos de categorías. Los científicos de datos a menudo usar variables de factor en su fórmula, porque las variables de categorías que los factores de control garantiza que los datos se procesa correctamente las funciones de aprendizaje de máquina. Para obtener más información, consulte [R guía básica sobre: Factor Variables] (http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/).

De forma predeterminada, se pueden convertir las variables de factor de cadenas en enteros y viceversa nuevo para el almacenamiento o procesamiento. El objeto R `data.frame` función controla todas las cadenas como variables de fases, a menos que el argumento *stringsAsFactors* está establecido en **False**. Esto significa que las cadenas son automáticamente es convertirse a un entero para el procesamiento y, a continuación, se asignan a la cadena original.

Si los datos de origen para factores se almacenan como un entero, rendimiento puede verse afectado, ya que R convierte a los enteros factor en cadenas en tiempo de ejecución y, a continuación, realiza su propia conversión de cadena a entero interno.

Para evitar estas conversiones en tiempo de ejecución, considere la posibilidad de almacenar los valores como enteros en la tabla de SQL Server y utilizar el _colInfo_ argumento para especificar los niveles de la columna que se utiliza como factor. Objetos de origen de datos la mayoría de RevoScaleR toman el parámetro _colInfo_. Este parámetro se usa para nombrar las variables usadas por el origen de datos, especificar su tipo y definir los niveles de las variables o transformaciones en los valores de columna.

Por ejemplo, la siguiente llamada de función de R obtiene los enteros 1, 2 y 3 de una tabla, pero asigna los valores para un factor con niveles "apple", "naranja" y "plátano".

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

Cuando la columna de origen contiene cadenas, siempre es más eficaz para especificar los niveles antes de tiempo mediante la _colInfo_ parámetro. Por ejemplo, el siguiente código R trata las cadenas como factores tal y como se leen.

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

Si no hay ninguna diferencia en la generación del modelo semántica, el último enfoque puede provocar un rendimiento mejor.

## <a name="data-transformations"></a>Transformaciones de datos

Los científicos de datos suelen emplear funciones de transformación escritas en R como parte del análisis. La función de transformación se aplica a cada fila que ha recuperado de la tabla. En SQL Server, estas transformaciones se aplican a todas las filas recuperadas en un lote, lo que requiere comunicación entre el intérprete de R y el motor de análisis. Para realizar la transformación, se mueven los datos de SQL al motor de análisis y, después, al proceso del intérprete de R y viceversa.

Por este motivo, el uso de transformaciones como parte del código R puede tener un efecto adverso significativo sobre el rendimiento del algoritmo, según la cantidad de datos implicados.

Es más eficaz tener todas las columnas necesarias en la tabla o vista antes de realizar el análisis, y evitar las transformaciones durante el cálculo. Si no es posible agregar más columnas a las tablas existentes, considere la posibilidad de crear otra tabla o vista con las columnas transformadas y usar una consulta adecuada para recuperar los datos.

## <a name="batch-row-reads"></a>Lee la fila de lote

Si utiliza un origen de datos de SQL Server (`RxSqlServerData`) en el código, se recomienda que intente usar el parámetro _rowsPerRead_ para especificar el tamaño del lote. Este parámetro define el número de filas que se consultan y, a continuación, se envía a la secuencia de comandos externo para su procesamiento. En tiempo de ejecución, el algoritmo puede ver solo el número especificado de filas en cada lote.

La capacidad de controlar la cantidad de datos que se procesan a la vez puede ayudarle a resolver o evitar problemas. Por ejemplo, si el conjunto de datos de entrada es muy grande (tiene muchas columnas), o si el conjunto de datos tiene unas pocas columnas de gran tamaño (por ejemplo, texto sin formato), puede reducir el tamaño del lote para evitar paginar datos no tiene memoria suficiente.

De forma predeterminada, el valor de este parámetro se establece a 50000, para garantizar un rendimiento aceptable incluso en equipos con poca memoria. Si el servidor tiene suficiente memoria disponible, al aumentar este valor a 500.000 o incluso un millón puede mejorar el rendimiento, especialmente para las tablas grandes.

Las ventajas de aumentar el tamaño de lote eran evidente en un conjunto de datos grande y en una tarea que se puede ejecutar en varios procesos. Sin embargo, al aumentar este valor no siempre generan los mejores resultados. Se recomienda que experimente con los datos y el algoritmo para determinar el valor óptimo.

## <a name="parallel-processing"></a>Procesamiento en paralelo

Para mejorar el rendimiento de **rx** funciones analíticas, puede aprovechar la capacidad de SQL Server para ejecutar tareas en paralelo mediante núcleos disponibles en el equipo del servidor.

Hay dos maneras para lograr la ejecución en paralelo con R en SQL Server:

-   **Use \@paralelas.** Cuando se usa el procedimiento almacenado `sp_execute_external_script` para ejecutar un script de R, se establece el parámetro `@parallel` en `1`. Este es el mejor método si el script de R no **no** usar funciones de RevoScaleR, que tienen otros mecanismos para su procesamiento. Si la secuencia de comandos utiliza funciones de RevoScaleR (generalmente con el prefijo "rx"), el procesamiento en paralelo se realiza automáticamente y no es necesario establecer explícitamente `@parallel` a `1`.

    Si el script de R se puede ejecutar en paralelo, y la consulta SQL se puede ejecutar en paralelo, el motor de base de datos crea varios procesos en paralelo. El número máximo de procesos que pueden crearse es igual que el **grado máximo de paralelismo** configuración (MAXDOP) para la instancia. Todos los procesos, a continuación, ejecutan la misma secuencia de comandos, pero solo una parte de los datos de recepción.
    
    Por lo tanto, este método no es útil con secuencias de comandos que se deben ver todos los datos, como cuando un modelo de entrenamiento. Pero resulta útil al realizar tareas como la predicción por lotes en paralelo. Para obtener más información sobre el uso de paralelismo con `sp_execute_external_script`, consulte el **avanzada sugerencias: procesamiento en paralelo** sección de [mediante código de R en Transact-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md).

-   **Usar numTasks = 1.** Cuando se usa **rx** funciones en un contexto de proceso de SQL Server, establezca el valor de la _numTasks_ parámetro para el número de procesos que desea crear. El número de procesos creados nunca puede ser más de **MAXDOP**; sin embargo, se determina el número real de los procesos creados por el motor de base de datos y puede ser menor de lo que solicita.

    Si el script de R se puede ejecutar en paralelo, y la consulta SQL se puede ejecutar en paralelo, SQL Server crea varios procesos en paralelo, al ejecutar las funciones de recepción. El número real de los procesos que se crean depende de una serie de factores como la regulación de recursos, el uso actual de recursos, otras sesiones y el plan de ejecución de consulta para la consulta utilizada con el script de R.

## <a name="query-parallelization"></a>Paralelización de consultas

En Microsoft R, puede trabajar con orígenes de datos de SQL Server mediante la definición de los datos como un objeto de origen de datos de RxSqlServerData.

Crea un origen de datos basado en una tabla o vista completa:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

Crea un origen de datos basado en una consulta SQL:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> Si se especifica una tabla en el origen de datos en lugar de una consulta, R Services usa heurística interna para determinar las columnas necesarias para capturar de la tabla. Sin embargo, este enfoque es poco probable que resulta en que la ejecución en paralelo.

Para asegurarse de que se pueden analizar los datos en paralelo, la consulta utilizada para recuperar los datos debe configurarse de tal manera que el motor de base de datos puede crear un plan de consulta en paralelo. Si el código o el algoritmo utiliza grandes volúmenes de datos, asegúrese de que la consulta da a `RxSqlServerData` está optimizado para la ejecución en paralelo. Una consulta que no da como resultado un plan de ejecución en paralelo puede producir un único proceso para el cálculo.

Si necesita trabajar con grandes conjuntos de datos, use Management Studio o el otro analizador de consultas SQL antes de ejecutar código R, para analizar el plan de ejecución. A continuación, tome las medidas recomendadas para mejorar el rendimiento de la consulta. Por ejemplo, un índice que falta en una tabla puede afectar al tiempo necesario para ejecutar una consulta. Para obtener más información, consulte [supervisión y optimización del rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md).

Otro error común que puede afectar al rendimiento es que una consulta recupera columnas de más de los necesarios. Por ejemplo, si una fórmula se basa en solo tres columnas, pero la tabla de origen tiene 30 columnas, va a mover datos innecesariamente.

 + Evite el uso de `SELECT *`!
 + Tardar algún tiempo para revisar las columnas del conjunto de datos e identificar solo los necesarios para el análisis
 + Quite las consultas de las columnas que contienen tipos de datos que no son compatibles con el código de R, tales como GUID y rowguid
 + Comprobación de no compatible formatos de fecha y hora
 + En lugar de cargar una tabla, crear una vista que selecciona ciertos valores o convierte columnas para evitar errores de conversión

## <a name="optimizing-the-machine-learning-algorithm"></a>Optimizar el algoritmo de aprendizaje de máquina

Esta sección proporciona varias sugerencias y recursos que son específicos de RevoScaleR y otras opciones de Microsoft R.

> [!TIP]
> Una discusión general de la optimización de R está fuera del ámbito de este artículo. Sin embargo, si tiene que hacer el código sea más rápida, se recomienda el artículo popular, [el Inferno R](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf). Cubre los errores comunes en detalle y colores vivos lenguaje y construcciones de programación en R y proporciona muchos ejemplos específicos de R técnicas de programación.

### <a name="optimizations-for-revoscaler"></a>Optimizaciones para RevoScaleR

Muchos algoritmos de RevoScaleR admiten parámetros para controlar cómo se genera el modelo entrenado. Aunque la precisión y la exactitud del modelo es importante, el rendimiento del algoritmo podría ser igualmente importante. Para obtener el equilibrio adecuado entre la precisión y el tiempo de entrenamiento, puede modificar los parámetros para aumentar la velocidad de cálculo y en muchos casos, mejorar el rendimiento sin reducir la precisión o exactitud.

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`admite la `maxDepth` parámetro, que controla la profundidad del árbol de decisión. Como `maxDepth` es mayor, el rendimiento puede reducirse, por lo que es importante analizar las ventajas de aumentar la profundidad y que afecta negativamente al rendimiento.

    También puede controlar el equilibrio entre la precisión de complejidad y la predicción de tiempo mediante el ajuste de parámetros como `maxNumBins`, `maxDepth`, `maxComplete`, y `maxSurrogate`. Aumentar la profundidad por encima de 10 o 15 puede hacer que el cálculo sea muy costoso.

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    Pruebe a usar el `cube` argumento si la primera variable dependiente en la fórmula es una variable de factor.
    
    Cuando `cube` se establece en `TRUE`, la regresión se realiza mediante un inverso con particiones, que podría ser más rápido y utiliza menos memoria que el cálculo de regresión estándar. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser significativa.

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    Use la `cube` argumento si la primera variable dependiente es una variable de factor.
    
    Cuando `cube` se establece en `TRUE`, el algoritmo utiliza un inversa con particiones, que podría ser más rápido y utiliza menos memoria. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser significativa.

Para obtener orientación adicional acerca de la optimización de RevoScaleR, vea estos artículos:

+ Artículo de soporte técnico: [rendimiento opciones de optimización de rxDForest y rxDTree](https://support.microsoft.com/kb/3104235)

+ Métodos para controlar el modelo caben en un modelo de árbol incrementado: [estimar modelos utilizando estocástico impulso de gradiente](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ Información general sobre cómo RevoScaleR mueve y procesa los datos: [escribir algoritmos personalizados de fragmentación en ScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ Modelo de programación para RevoScaleR: [administración de subprocesos en RevoScaleR](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ Función referencia para [rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ Función referencia para [rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Usar MicrosoftML

También se recomienda que muestran en el nuevo **MicrosoftML** paquete, que proporciona algoritmos de aprendizaje de máquina escalable que pueden usar los contextos de proceso y las transformaciones proporcionadas por RevoScaleR.

+ [Empezar a trabajar con MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [Cómo elegir un algoritmo de MicrosoftML](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>Incorporación de operatividad a una solución mediante Microsoft R Server

Si su escenario implica rápido predicción usando un modelo almacenado o integra el aprendizaje automático en una aplicación, puede usar el [puesta en marcha](https://docs.microsoft.com/r-server/what-is-operationalization) características de Microsoft R Server (anteriormente conocido como DeployR).

+ Como un **científico de datos**, use la [mrsdeploy paquete](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package) compartir código de R con otros equipos, e integrar el análisis de R en aplicaciones web, escritorio, móviles y panel: [cómo publicar y administrar los servicios web de R en R Server](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ Como un **administrador**, obtenga información acerca de cómo administrar paquetes, supervisar los nodos de web y nodos de proceso y controlar la seguridad de los trabajos de R: [cómo interactúan y consumir servicios web en R](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>Artículos de esta serie

[Rendimiento para la optimización de R: Introducción](sql-server-r-services-performance-tuning.md)

[Ajuste del rendimiento de R - configuración de SQL Server](sql-server-configuration-r-services.md)

[Ajuste del rendimiento de R - R optimización del código y los datos](r-and-data-optimization-r-services.md)

[Ajuste del rendimiento: resultados del estudio de caso](performance-case-study-r-services.md)

