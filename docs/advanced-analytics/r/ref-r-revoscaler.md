---
title: Biblioteca de funciones de R de RevoScaleR
description: Introducción a la biblioteca de funciones de RevoScaleR en SQL Server 2016 R Services y SQL Server Machine Learning Services con R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b5dcd2f14d1a1d8e23a62be299b1ff6f41814041
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715061"
---
# <a name="revoscaler-r-library-in-sql-server"></a>RevoScaleR (biblioteca de R en SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**RevoScaleR** es una biblioteca de funciones de ciencia de datos de alto rendimiento de Microsoft. Las funciones admiten la importación de datos, la transformación de datos, el Resumen, la visualización y el análisis.

A diferencia de las funciones base de R, las operaciones de RevoScaleR se pueden realizar en conjuntos de datos muy grandes, en paralelo y en sistemas de archivos distribuidos. Las funciones pueden operar en conjuntos de valores que no caben en la memoria mediante fragmentación y reensamblar los resultados cuando se completan las operaciones.

Las funciones de RevoScaleR se indican con un prefijo **RX** o **RX** para que sean fáciles de identificar.

RevoScaleR sirve como plataforma para la ciencia de datos distribuidos. Por ejemplo, puede usar las transformaciones y contextos de proceso de RevoScaleR con los algoritmos de última generación en [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). También puede usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para ejecutar funciones base de R en paralelo.

## <a name="full-reference-documentation"></a>Documentación de referencia completa

La biblioteca **RevoScaleR** se distribuye en varios productos de Microsoft, pero el uso es el mismo si se obtiene la biblioteca en SQL Server u otro producto. Dado que las funciones son iguales, la [documentación de las funciones individuales de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) se publica en una sola ubicación en la [referencia de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft machine learning Server. Si hay algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

La biblioteca **RevoScaleR** se basa en R 3.4.3 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Servicios de aprendizaje de máquina SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Cliente de Microsoft R](set-up-a-data-science-client.md)

> [!NOTE]
> Las versiones completas del producto son solo de Windows, empezando por SQL Server 2017. La compatibilidad con Linux para **RevoScaleR** es nueva en [SQL Server vista previa de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría para darle una idea de cómo se usa cada una de ellas. También puede usar la [tabla de contenido](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para buscar funciones en orden alfabético.

## <a name="1-data-source-and-compute"></a>1: origen de datos y proceso

**RevoScaleR** incluye funciones para crear orígenes de datos y establecer la ubicación, o el *contexto de cálculo*, de dónde se realizan los cálculos. Un objeto de origen de datos es un contenedor que especifica una cadena de conexión, junto con el conjunto de datos que quiera, definido como una tabla, una vista o una consulta. No se admiten llamadas a procedimientos almacenados. En la tabla siguiente se enumeran las funciones relevantes para SQL Server escenarios.

En algunos casos, SQL Server y R usan tipos de datos diferentes. Para obtener una lista de las asignaciones entre los tipos de datos de SQL y R, vea [tipos de datos de r a SQL](r-libraries-and-data-types.md).

| Función| Descripción|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  Cree un objeto de contexto de cálculo SQL Server para enviar los cálculos a una instancia remota. Varias funciones **RevoScaleR** toman el contexto de cálculo como argumento. |
|[rxGetComputeContext / rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | Obtiene o establece el contexto de cálculo activo. |
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | Cree un objeto de datos basado en una consulta o tabla de SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxodbcdata) | Cree un origen de datos basado en una conexión ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxxdfdata) | Cree un origen de datos basado en un archivo XDF local. Los archivos XDF se usan a menudo para descargar los datos en memoria en el disco. Un archivo XDF puede ser útil cuando se trabaja con más datos de los que se pueden transferir de la base de datos en un lote, o más datos de los que caben en la memoria. Por ejemplo, si mueve regularmente grandes cantidades de datos de una base de datos a una estación de trabajo local, en lugar de consultar la base de datos varias veces para cada operación de R, puede usar el archivo XDF como un tipo de caché para guardar los datos localmente y, después, trabajar con ellos en el área de trabajo de R.|

> [!TIP]
> Si no está familiarizado con la idea de orígenes de datos o contextos de cálculo, se recomienda empezar con la [informática distribuida](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) en la documentación de Microsoft machine learning Server.

### <a name="perform-ddl-statements"></a>Realizar instrucciones DDL

Puede ejecutar instrucciones DDL desde R si tiene los permisos necesarios en la instancia y en la base de datos. Las siguientes funciones utilizan llamadas ODBC para ejecutar instrucciones DDL o recuperar el esquema de la base de datos.

| Función| Descripción|
| ------- | ---------- |
| [rxSqlServerTableExists y rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | Quitar una [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] tabla o comprobar la existencia de una tabla o un objeto de base de datos. |
| [rxExecuteSQLDDL](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | Ejecute un comando de lenguaje de definición de datos (DDL) que defina o manipule objetos de base de datos. Esta función no puede devolver datos y solo se usa para recuperar o modificar el esquema de objetos o los metadatos.|

## <a name="2-data-manipulation-etl"></a>2: manipulación de datos (ETL)

Después de crear un objeto de origen de datos, puede utilizar el objeto para cargar datos en él, transformar los datos o escribir nuevos datos en el destino especificado. En función del tamaño de los datos en el origen, también puede definir el tamaño del lote como parte del origen de datos y mover los datos en fragmentos.

| Función | Descripción |
|----------|-------------|
| [rxOpen-methods](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxopen-methods) | Comprueba si un origen de datos está disponible, abre o cierra un origen de datos, Lee los datos de un origen, escribe los datos en el destino y cierra un origen de datos.|
| [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) | Mueva los datos desde un origen de datos al almacenamiento de archivos o a una trama de datos.|
| [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) | Transforme los datos mientras los mueve entre orígenes de datos.|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3-funciones de gráficos

| Nombre de función | Descripción |
|---------------|-------------|
|[rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram)  |Crea un histograma a partir de los datos. | 
|[rxLinePlot](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlineplot) |Crea un gráfico de líneas a partir de los datos. | 
|[rxLorenz](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlorenz)  |Calcula una curva Lorenz que se puede trazar. | 
|[rxRocCurve](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Calcula y traza curvas ROC a partir de datos reales y previstos. | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4-estadísticas descriptivas

| Nombre de función | Descripción |
|---------------|-------------|
|[rxQuantile](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxquantile)<sup>*</sup> |Calcula el cuantiles aproximado para los archivos. xdf y las tramas de datos sin ordenar. | 
|[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)<sup>*</sup> |Estadísticas básicas de Resumen de datos, incluidos cálculos por grupo. No se admite la escritura de cálculos de grupo en el archivo. xdf. | 
|[rxCrossTabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |Tabulación cruzada basada en fórmulas de los datos. | 
|[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube)<sup>*</sup> |Tabulación cruzada basada en fórmulas alternativa diseñada para la representación eficaz que devuelve resultados del cubo. No se admite la escritura de resultados en el archivo. xdf. | 
|[rxMarginals](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxmarginals)  |Resúmenes marginales de las tabulaciones cruzadas. | 
|[as.xtabs](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/as.xtabs)  |Convierte los resultados de tabulación cruzada en un objeto xtabs. | 
|[rxChiSquaredTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Realiza una prueba chi cuadrado en el objeto xtabs. Se usa con conjuntos de datos pequeños y no fragmenta los datos. | 
|[rxFisherTest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Realiza la prueba exacta de Fisher en el objeto xtabs. Se usa con conjuntos de datos pequeños y no fragmenta los datos. | 
|[rxKendallCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |Calcula el coeficiente de correlación de rangos de Kendall con el objeto xtabs. | 
|[rxPairwiseCrossTab](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |Aplica una función a las combinaciones en pares de filas y columnas de un objeto xtabs. | 
|[rxRiskRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcular el riesgo relativo de un objeto xtabs de dos por dos. | 
|[rxOddsRatio](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxriskratio)  |Calcular la relación de probabilidades en un objeto xtabs de dos por dos. | 

<sup>*</sup>Indica las funciones más populares de esta categoría.

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5: funciones de predicción

| Nombre de función | Descripción |
|---------------|-------------|
|[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |Ajusta un modelo lineal a los datos. | 
|[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |Ajusta un modelo de regresión logística a los datos. | 
|[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |Ajusta un modelo lineal generalizado a los datos. | 
|[rxCovCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |Calcular la covarianza, la correlación o la suma de cuadrados/matriz de productos cruzados para un conjunto de variables. | 
|[rxDTree](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |Ajusta un árbol de clasificación o regresión a los datos. | 
|[rxBTrees](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |Se ajusta a un bosque de decisión de clasificación o regresión a los datos mediante un algoritmo de potenciación de gradiente estocástico. | 
|[rxDForest](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdforest)<sup>*</sup> |Se ajusta a los datos de un bosque de decisión de clasificación o regresión. | 
|[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxPredict)<sup>*</sup> |Calcula las predicciones para los modelos ajustados. La salida debe ser un origen de datos XDF. | 
|[rxKmeans](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxkmeans)<sup>*</sup> |Realiza la agrupación en clústeres k-means. | 
|[rxNaiveBayes](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |Realiza una clasificación Bayes Naive. | 
|[rxCov](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor) |Calcula la matriz de covarianza de un conjunto de variables. | 
|[rxCor](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcula la matriz de correlación de un conjunto de variables. | 
|[rxSSCP](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcovcor)  |Calcular la suma de cuadrados/matriz de productos cruzados para un conjunto de variables. | 
|[rxRoc](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxroc)  |Los cálculos de características operativas (ROC) del receptor con valores reales y previstos del sistema clasificador binario. | 

<sup>*</sup>Indica las funciones más populares de esta categoría.


## <a name="how-to-work-with-revoscaler"></a>Cómo trabajar con RevoScaleR

Las funciones de **RevoScaleR** se pueden llamar en código R encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones **RevoScaleR** localmente y, después, migran el código R finalizado a procedimientos almacenados como un ejercicio de implementación.

Cuando se ejecuta localmente, normalmente se ejecuta un script de R desde la línea de comandos o desde un entorno de desarrollo de R, y se especifica un contexto de proceso de SQL Server mediante una de las funciones de **RevoScaleR** . Puede usar el contexto de cálculo remoto para todo el código o para funciones individuales. Por ejemplo, puede que desee descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Cuando esté preparado para encapsular un script de R en un procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda volver a escribir el código como una sola función que tiene entradas y salidas claramente definidas. 

## <a name="see-also"></a>Vea también

+ [Tutoriales de R](../tutorials/sql-server-r-tutorials.md)
+ [Aprenda a usar contextos de cálculo](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desarrolladores de SQL: Entrenar y poner en funcionamiento un modelo](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Ejemplos de productos de Microsoft en GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referencia de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 
