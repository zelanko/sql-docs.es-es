---
title: "R y optimizaci&#243;n de datos (servicios de R) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# R y optimizaci&#243;n de datos (servicios de R)
Este tema describe los métodos para actualizar el código de R para mejorar el rendimiento o evitar problemas conocidos.

## Contexto de proceso

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Puede utilizar el __local__ o __SQL__ calcular contexto al realizar el análisis. Cuando se usa el __local__ contexto de cálculo, análisis se realiza en el equipo cliente y se deben recuperar los datos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] través de la red. El impacto en el rendimiento se incurre para esta transferencia de red depende del tamaño de los datos transferidos, velocidad de la red y otras transferencias de red que se producen al mismo tiempo.

Si el contexto del proceso es __SQL Server__, a continuación, las funciones analíticas se ejecutan dentro de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Los datos son locales a la tarea de análisis, por lo que no se introduce ninguna sobrecarga de la red. 

Cuando se trabaja con grandes conjuntos de datos, debe utilizar siempre el contexto del proceso SQL.

## Factores

El lenguaje R convierte las cadenas de tablas en factores. Tener muchos objetos de origen de datos `colInfo` como un parámetro para controlar cómo se tratan las columnas. Por ejemplo, `c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` se consumen enteros de 1, 2 y 3 de una tabla y tratarlos como factores con niveles de `apple`, `orange`, y `banana`. 

Los científicos de datos a menudo utilizan variables factor en su fórmula; Sin embargo, con factores cuando el origen de datos es un entero se afectado el rendimiento como números enteros se convierten en cadenas en tiempo de ejecución. Sin embargo, si la columna contiene las cadenas, puede especificar los niveles antes de tiempo mediante `colInfo`. En este caso, la instrucción equivalente sería  `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`, que trata las cadenas como factores como se leen. 

Para evitar conversiones en tiempo de ejecución, considere la posibilidad de almacenar los niveles como enteros en la tabla y consumirlos tal como se describe en el primer ejemplo. Si no hay ninguna diferencia en la generación del modelo semántica, este enfoque puede provocar un rendimiento mejor.

## Transformación de datos

Los científicos de datos suelen emplear funciones de transformación escritas en R como parte del análisis. Las funciones de transformación deben aplicarse a cada fila que se recuperan de la tabla. En [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], esta transformación tiene lugar en modo por lotes e implica una comunicación entre el intérprete de R y el motor de análisis. Para realizar la transformación, se mueven los datos de SQL para el motor de análisis y, a continuación, el proceso de intérprete de R y viceversa. Por lo tanto, con las transformaciones pueden tener como importante efecto adverso en el rendimiento del algoritmo, según la cantidad de datos implicados.

Es más eficaz que todas las columnas necesarias en la tabla o vista antes de realizar el análisis, como esto evita las transformaciones durante el cálculo. Si no es posible agregar más columnas a las tablas existentes, considere la posibilidad de crear otra tabla o vista con las columnas transformadas y usar una consulta adecuada para recuperar los datos.

## Procesar por lotes

El origen de datos SQL (`RxSqlServerData`) tiene una opción para indicar el tamaño de lote mediante el parámetro `rowsPerRead`. Este parámetro especifica el número de filas que se van a procesar a la vez. En tiempo de ejecución, algoritmos leerá especificado con el número de filas en cada lote. De forma predeterminada, el valor de este parámetro se establece en 50.000, para asegurarse de que los algoritmos pueden realizar correctamente incluso en equipos con poca memoria. Si el equipo tiene suficiente memoria disponible, al aumentar este valor a 500.000 o incluso un millón puede mejorar el rendimiento, especialmente para las tablas grandes. 

Al aumentar este valor no siempre puede producir resultados mejores y puede requerir algún tipo de experimentación para determinar el valor óptimo. Las ventajas de esto será más evidentes en un gran conjunto de datos con varios procesos (`numTasks` establecido en un valor mayor que `1`).

## Procesamiento paralelo

Para mejorar el rendimiento de la ejecución de funciones analíticas dentro de rx [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] se basa en el procesamiento en paralelo con los núcleos disponibles en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] automático. Hay dos formas de lograr la ejecución en paralelo con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:

* Cuando se usa el `sp_execute_external_script` procedimiento almacenado para ejecutar un script de R, establecer el `@parallel` parámetro `1`. Esto es útil para los scripts de R que no utilizan funciones RevoScaleR, que generalmente tienen el prefijo "rx". Si la secuencia de comandos utiliza las funciones RevoScaleR, procesamiento en paralelo se controla automáticamente y no debe establecer `@parallel` a `1`.

    Si el script de R se puede ejecutar en paralelo y el [!INCLUDE[tsql_md](../../includes/tsql-md.md)] se puede paralelizar consulta, a continuación, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] creará varios procesos en paralelo (hasta el __grado máximo de paralelismo MAXDOP__ para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)],) y ejecutar la misma secuencia de comandos a través de todos los procesos. Cada proceso recibe sólo una parte de los datos, por lo que esto no es útil con secuencias de comandos que se deben ver todos los datos, como al entrenar un modelo. Sin embargo, resulta útil al realizar tareas como la predicción por lotes en paralelo. Para obtener más información sobre el uso de paralelismo con [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), consulte el __sugerencias avanzada: procesamiento paralelo__ sección de [utilizando código R en Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md).

* Al utilizar las funciones de recepción con un contexto de proceso de SQL Server, establezca `numTasks` en el número de procesos que desea crear. Se determina el número real de los procesos creados por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], y puede ser menor que el solicitado. El número de procesos creados nunca puede ser más de __MAXDOP__.

    Si el script de R se puede ejecutar en paralelo y el [!INCLUDE[tsql_md](../../includes/tsql-md.md)] se puede paralelizar consulta, a continuación, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] creará varios procesos en paralelo cuando se ejecuta las funciones de recepción.

El número de procesos que va a crear depende de diversos factores, como el regulador de recursos, uso actual de recursos, otras sesiones y el plan de ejecución de consulta para la consulta utilizada con el script de R. 

### Paralelización de consultas

Para asegurarse de que se pueden analizar los datos en paralelo, la consulta utilizada para recuperar los datos debe configurarse de tal forma que puede representar para la ejecución en paralelo. 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite trabajar con orígenes de datos SQL mediante `RxSqlServerData` para especificar el origen. El origen puede ser una tabla o una consulta. Por ejemplo, ejemplos de código siguientes definen un objeto de origen de datos R basado en una consulta SQL:
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

Los algoritmos de análisis tire de grandes volúmenes de datos de las tablas, es importante asegurarse de que la consulta proporcionada a `RxSqlServerData` está optimizado para la ejecución en paralelo. Una consulta que no da como resultado un plan de ejecución en paralelo puede producir un único proceso para el cálculo.

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] puede utilizarse para analizar el plan de ejecución y mejorar el rendimiento de la consulta. Por ejemplo, un índice que falta en una tabla puede afectar al tiempo necesario para ejecutar una consulta. Consulte [supervisar y optimizar el rendimiento](../../relational-databases/performance/monitor-and-tune-for-performance.md) para obtener más información.

Supervisión de otra que puede afectar al rendimiento es cuando la consulta recupera columnas de más de los necesarios. Por ejemplo, si una fórmula se basa en 3 columnas y la tabla tiene 30 columnas, no utilice una consulta como `select *` o uno que selecciona columnas de más de lo necesario.

> [!NOTE]
> Si se especifica una tabla en el origen de datos en lugar de una consulta, [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] internamente determinará las columnas necesarias para capturar de la tabla; sin embargo, este enfoque es poco probable que resulta en la ejecución en paralelo.

## Parámetros de algoritmo

Muchos algoritmos de aprendizaje rx admiten parámetros para controlar cómo se genera el modelo de entrenamiento. Aunque la precisión y la exactitud del modelo es importante, el rendimiento del algoritmo puede ser igualmente importante. Puede modificar los parámetros de entrenamiento del modelo de paquetesEn para aumentar la velocidad de cálculo y, en muchos casos, puede mejorar el rendimiento sin reducir la precisión o la corrección. 

Por ejemplo, `rxDTree` es compatible con la `maxDepth` parámetro, que controla la profundidad de árbol. Como `maxDepth` es aumenta, el rendimiento puede disminuir, por lo que es importante analizar las ventajas de aumentar la profundidad y el impacto de rendimiento. 

Uno de los parámetros que se pueden usar con `rxLinMod` y `rxLogit` es el `cube` argumento. Este argumento se puede utilizar cuando la primera variable dependiente de la fórmula es una variable de factor. Si `cube` se establece en `TRUE`, la regresión se realiza mediante un inverso con particiones, puede ser más rápido y utilizan menos memoria que el cálculo de regresión estándar. Si la fórmula tiene un gran número de variables, la ganancia de rendimiento puede ser importante.

El [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) Guía del usuario tiene información útil para controlar el modelo se ajusta a distintos algoritmos. Por ejemplo, con `rxDTree` puede controlar el equilibrio entre la precisión de complejidad y la predicción del tiempo mediante el ajuste de parámetros como `maxNumBins`, `maxDepth`, `maxComplete`, y `maxSurrogate`. Al aumentar la profundidad a más allá de 10 o 15 para hacer el cálculo muy costosa.

Para obtener más información acerca del ajuste de rendimiento para `rxDForest` y `rxDTree`, consulte [rendimiento opciones de optimización de rxDForest/rxDTree](https://support.microsoft.com/kb/3104235).

## Modelo y predicción

Una vez se ha completado el entrenamiento y el mejor modelo seleccionado, se recomienda almacenar el modelo en la base de datos para que esté disponible para las predicciones. Procesamiento de transacciones en línea que requiere la predicción, cargar el modelo previamente calculado de la base de datos para la predicción es muy eficaz. Las secuencias de comandos de ejemplo utilizan este enfoque para serializar y almacenar el modelo en una tabla de base de datos. Para la predicción, el modelo se deserializa desde la base de datos.

Algunos modelos generados por algoritmos como lm o glm pueden ser bastante grandes, especialmente cuando se utiliza en un gran conjunto de datos. Existen limitaciones de tamaño para los datos que pueden almacenarse en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Debería limpiar el modelo antes de almacenar la base de datos.

> [!NOTE] Si la predicción rápida con un modelo almacenado y el análisis a integrar en una aplicación es un escenario importante, se recomienda __DeployR__. Puede usar para integrar fácilmente análisis de R en aplicaciones web, escritorio, móviles y panel. En concreto, es ideal para almacenar un modelo y, a continuación, realizar la predicción de fila utilizando el modelo almacenado. Para obtener más información, consulte [DeployR sobre](https://msdn.microsoft.com/microsoft-r/rserver/deployr-about).

## Vea también
[Gobierno de recursos](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)

[CREAR GRUPO DE RECURSOS EXTERNOS](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [Guía de optimización de rendimiento de SQL Server R servicios](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [Configuración de SQL Server para los servicios de R](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [Caso práctico de rendimiento](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 